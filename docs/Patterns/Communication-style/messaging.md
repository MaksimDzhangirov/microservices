# Шаблон: Обмен сообщениями

[Оригинал](https://microservices.io/patterns/communication-style/messaging.html)

## Дано

## Дополнительные условия

## Задача

## Решение

## Примеры

## Преимущества и недостатки

## Связанные шаблоны

* [Шаблон Saga] и [шаблон CQRS] используют обмен сообщениями
* [Шаблон Таблица исходящих транзакций]() позволяет отправлять сообщения 
  как часть транзакции базы данных
* [Шаблон Внешняя конфигурация] задаёт (логические) названия каналов сообщений 
  и расположение брокера сообщений
* Шаблон [Протокол, специфичный для предметной области](domain-specific-protocol.md) является 
  альтернативным шаблоном
* Шаблон [Удаленный вызов процедуры](rpi.md) является альтернативным шаблоном

## Смотри также

* В моей книге [Microservices patterns](https://microservices.io/book) подробно 
  описывается межсервисное взаимодействие
* На сайте [Шаблоны корпоративной интеграции](http://www.enterpriseintegrationpatterns.com/) подробно 
  описываются шаблоны обмена сообщениями
* [Фреймворк Event Tram](http://eventuate.io/), реализует транзакционный 
  обмен сообщениями для микросервисов