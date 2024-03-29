# Шаблон: По сервису на контейнер

[Оригинал](https://microservices.io/patterns/deployment/service-per-container.html)

## Дано

Вы воспользовались шаблоном [Микросервисная архитектура](../Application-architecture-patterns/pattern-microservice-architecture.md) и
спроектировали свою систему как набор сервисов. Каждый сервис развертывается
как набор экземпляров сервиса для обеспечения пропускной способности и
доступности.

## Задача

Как оформить и развернуть сервисы?

## Дополнительные условия

* Сервисы написаны с использованием различных языков, фреймворков и
  версий фреймворков
* Каждый сервис состоит из нескольких экземпляров сервиса для обеспечения
  пропускной способности и доступности
* Сервис должен быть независимо развертываемым и масштабируемым
* Экземпляры сервиса должны быть изолированы друг от друга
* Вам нужно уметь быстро создавать и развертывать сервис
* Вы должны иметь возможность ограничивать ресурсы (ЦП и память),
  потребляемые сервисом.
* Вам необходимо отслеживать поведение каждого экземпляра сервиса
* Вы хотите, чтобы развертывание было надежным
* Вы должны развернуть приложение как можно более экономично

## Решение

Оформите сервис в виде образа (Docker) контейнера и разверните каждый
экземпляр сервиса как контейнер

## Примеры

Docker становится чрезвычайно популярным способом оформления и 
развертывания сервисов. Каждый сервис оформлен в виде Docker образа, а 
каждый экземпляр сервиса представляет собой Docker контейнер. Существует 
несколько сред Docker кластеризации, в том числе:

* [Kubernetes](http://kubernetes.io/)
* [Marathon/Mesos](https://mesosphere.github.io/marathon/)
* [Сервис для работы с контейнерами Amazon EC2](http://aws.amazon.com/ecs/)

## Преимущества и недостатки

К преимуществам такого подхода относятся:

* Можно легко масштабировать сервис в большую или меньшую сторону, изменив 
  количество экземпляров контейнера
* Контейнер инкапсулирует детали технологии, используемой для создания 
  сервиса. Например, все сервисы запускаются и останавливаются одинаково
* Каждый экземпляр сервиса изолирован
* Контейнер накладывает ограничения на ЦП и память, потребляемые 
  экземпляром сервиса
* Контейнеры очень быстро собираются и запускаются. Например, оформить 
  приложение в виде Docker контейнер в 100 раз быстрее, чем как AMI. 
  Docker контейнеры также запускаются намного быстрее, чем виртуальная 
  машина, поскольку запускается только процесс приложения, а не вся ОС
  
К недостаткам этого подхода относятся:

* Инфраструктура для развертывания контейнеров не так богата, как 
  инфраструктура для развертывания виртуальных машин

## Связанные шаблоны

* Этот шаблон является усовершенствованием [шаблона «По сервису на хосте»](single-service-per-host.md)
* [Шаблон «По сервису на виртуальной машине»](service-per-vm.md) является 
  альтернативным решением.
* [Шаблон «Бессерверное развертывание»](serverless-deployment.md) является 
  альтернативным решением.