# Шаблон: Таблица исходящих транзакций

[Оригинал](https://microservices.io/patterns/data/transactional-outbox.html)

## Также известен как

События приложения

## Дано

От команды сервиса обычно требуется обновить базу данных **и** отправить
сообщения/события. Например, сервис, участвующий в [саге](../../Data-management/saga.md), должен
автоматически обновлять базу данных и отправлять сообщения/события. Точно
так же сервис, который публикует [событие предметной области](../../Data-management/domain-event.md), должен
атомарно обновлять [агрегат](../../Data-management/aggregate.md) и публиковать событие.

Сервис должен автоматически обновлять базу данных и отправлять сообщения,
чтобы избежать несоответствий данных и ошибок. Однако нецелесообразно
использовать традиционную распределенную транзакцию (2PC), которая
охватывает базу данных и брокер сообщений для атомарного обновления базы
данных и публикации сообщений/событий. Брокер сообщений может не
поддерживать 2PC. И даже если это так, часто нежелательно связывать сервис
как с базой данных, так и с сообщением.

Но без использования 2PC отправка сообщения в середине транзакции
ненадежна. Нет никакой гарантии, что транзакция будет зафиксирована. Точно
так же, если сервис отправляет сообщение после фиксации транзакции, нет
гарантии, что он не выйдет из строя до отправки сообщения.

Кроме того, сообщения должны отправляться брокеру сообщений в том порядке,
в котором они были отправлены сервисом. Обычно они должны доставляться
каждому потребителю в одном и том же порядке, хотя это выходит за рамки
данного шаблона. Например, предположим, что агрегат обновляется серией
транзакций `T1`, `T2` и т. д. Эти транзакции могут осуществляться одним и
тем же экземпляром сервиса или разными экземплярами сервиса. Каждая
транзакция публикует соответствующее событие: `T1 -> E1`, `T2 -> E2` и
т. д. Поскольку `T1` предшествует `T2`, событие `E1` должно быть опубликовано
до `E2`.

## Задача

Как надежно/атомарно обновлять базу данных и отправлять сообщения/события?

## Дополнительные условия

* [2PC](https://en.wikipedia.org/wiki/Two-phase_commit_protocol) использовать не вариант
* Если транзакция базы данных фиксируется, сообщения должны быть отправлены.
  И наоборот, если база данных откатывается, сообщения не должны отправляться
* Сообщения должны отправляться брокеру сообщений в том порядке, в котором
  они были отправлены сервисом. Этот порядок должен сохраняться для случая,
  когда несколько экземпляров сервиса обновляют один и тот же агрегат

## Решение

Сервис, использующий реляционную базу данных, вставляет сообщения/события 
в таблицу исходящих сообщений (например, `MESSAGE`) как часть локальной 
транзакции. Сервис, использующий NoSQL базу данных, добавляет 
сообщения/события к атрибуту обновляемой записи (например, документа или 
элемента). Отдельный процесс _Ретрансляции Сообщений_ публикует события, 
вставленные в базу данных, в брокер сообщений.

![](../../../images/transactional-outbox/ReliablePublication.png)

## Преимущества и недостатки

Этот шаблон имеет следующие преимущества:

* 2PC не используется
* Сообщения гарантированно отправляются тогда и только тогда, когда 
  транзакция базы данных фиксируется
* Сообщения отправляются брокеру сообщений в том порядке, в котором они 
  были отправлены приложением

Этот шаблон имеет следующие недостатки:

* Потенциально подвержен ошибкам, поскольку разработчик может забыть 
  опубликовать сообщение/событие после обновления базы данных

Этот шаблон также имеет следующие проблемы:

* _Ретранслятор Сообщений_ может опубликовать сообщения более одного раза. 
  Например, он может аварийно завершать работу после публикации сообщения, 
  но до того, как это будет зафиксировано. Когда он перезапустится, он 
  снова опубликует сообщение. В результате подписчик сообщений должен 
  быть идемпотентным, возможно, путем отслеживания идентификаторов 
  сообщений, к тем, которые он уже обработал. К счастью, поскольку
  подписчики сообщений обычно должны быть идемпотентными (поскольку 
  брокер сообщений может доставлять сообщения более одного раза), обычно это 
  не является проблемой.

## Связанные шаблоны

* Шаблоны [Сага](../../Data-management/saga.md) и [Событие предметной области](../../Data-management/domain-event.md) создают
  необходимость использования этого шаблона
* [Генерация событий](../../Data-management/event-sourcing.md) является 
  альтернативным решением
* Существует два шаблона для реализации ретрансляции сообщений:
  * Шаблон [Отслеживание лога транзакций](transaction-log-tailing.md)
  * Шаблон [Отправка сообщений путём опрашивания](polling-publisher.md)

## Где можно получить более подробную информацию о шаблоне

* В моей книге [Microservices patterns](https://microservices.io/book) этот 
  шаблон описывается подробнее.
* В [фреймворке Eventuate Tram](https://github.com/eventuate-tram/eventuate-tram-core)
  реализован этот шаблон