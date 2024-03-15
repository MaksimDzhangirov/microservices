# Шаблон: API-шлюз / Бэкенды для фронтендов

[Оригинал](https://microservices.io/patterns/apigateway.html)

## Дано

## Задача

## Дополнительные условия

## Решение

![](../../../images/api-gateway/apigateway.jpg)

## Одна из возможных реализаций: Бэкенды для фронтендов

![](../../../images/api-gateway/bffe.png)

## Примеры

* [API-шлюз Netflix](http://techblog.netflix.com/2013/01/optimizing-netflix-api.html)
* Простой [шлюз Java/Spring API](https://github.com/cer/event-sourcing-examples/tree/master/java-spring/api-gateway-service)
  из [примера приложения Money Transfer](https://github.com/cer/event-sourcing-examples)

## Преимущества и недостатки

## Связанные шаблоны

* [Шаблон Микросервисная архитектура](../Application-architecture-patterns/pattern-microservice-architecture.md) 
  создает необходимость использования этого шаблона
* API-шлюз должен использовать шаблон [Обнаружения на стороне клиента]() или 
  шаблон [Обнаружения на стороне сервера]() для маршрутизации запросов к 
  доступным экземплярам сервиса
* API-шлюз может аутентифицировать пользователя и передавать [токен доступа](), 
  содержащий информацию о пользователе, сервисам
* API-шлюз будет использовать [Circuit Breaker]() 
  для вызова сервисов
* API-шлюз часто реализует шаблон [Композиция API](../../Data-management/api-composition.md)

## Известные компании, использующие данный шаблон

* [API-шлюз Netflix](http://techblog.netflix.com/2012/07/embracing-differences-inside-netflix.html)

## Пример приложения

Смотри API-шлюз, который является частью [примера приложения](https://github.com/microservice-patterns/ftgo-application)
из моей книги Microservices pattern. Он реализован, используя Spring Cloud 
Gateway.