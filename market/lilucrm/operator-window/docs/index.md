# Единое окно - система автоматизации работы колл-центра Маркета

Единое окно - инструмент операторов колл-центра Маркета для обработки входящих обращений поступающих по разнообразным
каналам, таким как телефония, электронная почта, чаты и др.

В основе системы лежит платформа для автоматизации бизнес-процессов, позволяющая в декларативном виде описывать
хранимую информацию, а так же автоматизировать бизнес-логику модификации бизнес-объектов.

## Хранение данных

Основным хранилищем данных является реляционная база работа с которой осуществляется с помощью ORM
[Hibernate](https://hibernate.org/orm/). Наша система работает с [PostgresQL](https://www.postgresql.org/) и использует
его специфичные возможности, например, [JSONB](https://www.postgresql.org/docs/13/datatype-json.html) тип колонок.

Так же мы умеем интегрироваться с произвольными сервисам по HTTP и получать данные из них, но возможностей по
автоматизации для данных полученных таким образом меньше.

## Конфигурирование системы { #metadata }

Все бизнес-объекты системы описаны [метаинформацией](metadata/index.md), что позволяет унифицировать операции с
бизнес-объектами, интерфейс пользователя системы, а так же АПИ для интеграции с внешними системами. Так же
есть возможность настраивать [жизненный цикл](metadata/wf.md) бизнес-объектов.

## Архитектура

![Архитектура](_imgs/arch.png "Архитектура" =860x500)

## Дополнительные материалы

1. Вводный рассказ [видео](https://moderator.video.yandex-team.ru/m/film-info?service=video-nda&n=7546).
1. Рассказ об устройстве фронтенда [видео 1](https://jing.yandex-team.ru/files/loudless/Встреча%20№1.1530fa2.mp4),
 [видео 2](https://jing.yandex-team.ru/files/loudless/Встреча%20№2.mp4),
 [видео 3](https://disk.yandex.ru/public/nda/?hash=oLFRNjHNcfOxlv5K8JES60RaHXMwilWzse3NRH8RCau2hAwpWx9FZf3KzsjL1jgpq/J6bpmRyOJonT3VoXnDag%3D%3D).
1. [Набор](https://wiki.yandex-team.ru/market/development/operator-window/Testing-operator-window/Znakomstvo-s-sistemojj-i-prakticheskie-zadanija/) заданий для знакомства с системой.
1. Рассказ про чаты [видео 1](https://moderator.video.yandex-team.ru/m/film-info?service=video-nda&n=7544), [видео 2](https://moderator.video.yandex-team.ru/m/film-info?service=video-nda&n=7545).



