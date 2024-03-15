# Шаблон: Удаленный вызов процедуры

[Оригинал](https://microservices.io/patterns/communication-style/rpi.html)

## Дано

## Дополнительные условия

## Задача

## Решение

## Примеры

## Преимущества и недостатки

## Связанные шаблоны

* [Протокол, специфичный для предметной области](domain-specific-protocol.md) является альтернативным 
  шаблоном
* [Обмен сообщениями](messaging.md) — это альтернативный шаблон
* [Внешняя конфигурация](../Cross-cutting-concerns/externalized-configuration.md) задаёт 
  (логическое) сетевое расположение, например, URL сервиса.
* Клиент должен использовать либо [Обнаружение на стороне клиента](), либо [Обнаружение 
  на стороне сервера](), чтобы найти экземпляр сервиса.
* Клиент обычно использует [шаблон Circuit Breaker]() для повышения надежности.