# baker

## Что и зачем.

Набор общих компонентов для сервисов, написанных с использованием [cake-pattern](https://habr.com/ru/post/68633/).

Данная библиотека призвана упростить создание новых сервисов в Вертикалях. Конкретно в Вертикалях: содержит специфичные для нашего стека вещи, обычно кочующие из сервиса в сервис.

<details>
<summary>Какие-такие сервисы?</summary>

Все сервисы в основном можно разделить на два вида: апи (или realtime service) и шедулер (или non-realtime service). Апи - то, что умеет отвечать на внешние запросы. Шедулер - то, что на запросы не отвечает, а наоборот, периодически само делает какую-то работу. Обычно, чтобы сервис успешно поселился в номад, умел работать в виде многих инстансов, был наблюдаемым и расширяемым, нужно проделать ряд одних и тех же действий. В бейкере есть средства для быстрой реализации и того и другого видов сервисов.

</details>

Baker берет на себя:
* Чтение конфигурации из датасорсов с поддержкой разных типов окружения (dev, test, prod)
* Поддержка трейсинга в jaeger
* Поддержка метрик в prometheus
* Фреймворк для периодических операций
* Распределение работы между различными инстансами шедулера
* Загрузка ext data types через s3edr
* Поддержка Http Async Client
* Поддержка работы с зукипером
* Поддержка фич на основе зукипера
* Логирование с учетом трейсов и передачей их в "новые логи"
* Простые запросы в базы данных
* Работа с ydb

и многое другое.

Описанные вещи не подвешены в воздухе, а тесно связаны между собой: читают нужные им конфиги, пишут логи и метрики унифицированным образом. Пользователю библиотеки остается как из кирпичиков собрать нужный набор из готовых компонентов и по сути из коробки получить production-ready приложение (пишущее логи, отправляющее метрики, правильно реагирующее на сигналы итд), требущее минимальной донастройки в части бойлерплейта. Благодаря этому можно быстро перейти к написанию сути сервиса.

Кроме того, в библиотеку добавлены средства:
* Упрощающие работу с зукипером: [ZookeeperInterface](https://github.com/YandexClassifieds/baker/blob/ecc6eb00907ab966a6e6ecce8a409a527aefaa3c/src/main/scala/ru/yandex/vertis/baker/components/zookeeper/zkinterface/ZookeeperInterface.scala), [ZookeeperNode](https://github.com/YandexClassifieds/baker/blob/a23b7989aee68e056f12be5fad8d9e74051204f4/src/main/scala/ru/yandex/vertis/baker/components/zookeeper/node/ZookeeperNode.scala)
* Облегчающие конфигурирование http клиентов: [HttpClientBuilder](https://github.com/YandexClassifieds/baker/blob/eb522fa0567d0b4851b212cd95f9e713f8756990/src/main/scala/ru/yandex/vertis/baker/components/http/client/HttpClientBuilder.scala), [HttpClientConfigBuilder](https://github.com/YandexClassifieds/baker/blob/06f1782c57944333d5c5c8712036c3146de57973/src/main/scala/ru/yandex/vertis/baker/components/http/client/config/HttpClientConfigBuilder.scala)
* Всевозможные [директивы апи](https://github.com/YandexClassifieds/baker/tree/7d57800cfbe4c02085dc9951f605c2270380e349/src/main/scala/ru/yandex/vertis/baker/util/api/directives)
* [Настройка](https://github.com/YandexClassifieds/baker/blob/628e66c29d538d00759fd494c639338e2affcf17/src/main/scala/ru/yandex/vertis/baker/util/workmoments/WorkMoments.scala) точного времени запуска периодических задач
* А также хелперные функции для работы с конфигами, датой и временем, строками, трейсами

и так далее

Для успешного выполнения этой задачи библиотека фиксирует определенный набор используемых зависимостей и их версий. И это ограничение накладывается и на клиентский код. Baker собран под scala 2.12, использует vertis-scala-common 2.0.48, библиотека api: akka-http + swagger, шедулер: самописный фреймворк WorkersFactory (родом из воса, несколько модифицированный), итд. Предпринята работа по исключению конфликтов используемых зависимостей.

Однако, модульная структура, лежащая в основе библиотеки (и cake-pattern) позволяет легко добавлять и изменять используемые в работе компоненты.

## Примеры.

* [Story-api](https://github.com/YandexClassifieds/story-api): api, sbt
* [Autoru-Chat-Bot](https://github.com/YandexClassifieds/autoru-chat-bot): api и scheduler, maven
* [Vos2-Autoru-Mirror](https://github.com/YandexClassifieds/vos2-autoru/tree/932011c02287db4310b01b49ae29f2ffef43819d/vos2-autoru-mirror): scheduler, maven
* [Autoru-Catalog](https://github.com/YandexClassifieds/autoru-catalog): api, maven

Простейшие примеры сервисов, полностью помещающихся в одном файле, можно найти в тестах:
* [ApiTest](https://github.com/YandexClassifieds/baker/blob/5a7d42c35e2ea369fed3e01490cd5a561d416697/src/test/scala/ru/yandex/vertis/baker/ApiTest.scala): пример апи. Поднимается на 5000 порту (прометеус на 5001), отвечает на /spi/ping. Данный пример является полностью функциональным: у него есть ручка ping, метрики апи, сваггер, трейсинг
* [SchedulerTest](https://github.com/YandexClassifieds/baker/blob/5a7d42c35e2ea369fed3e01490cd5a561d416697/src/test/scala/ru/yandex/vertis/baker/SchedulerTest.scala): пример шедулера. Раз в 100 миллисекунд инкрементит переменную, пока она не достигнет значения 5. Также воркер production-ready: имеет метрики и логи времени работы и ошибок, заметерен тред пул, на котором он крутится, через token distribution происходит масштабирование на инстансы (при желании воркер будет работать только на одном, либо можно распределить работу хитрее). Здесь же пример легкой замены одного компонента другим: сервер прометеуса на 5001 порту уже поднят в ApiTest, поэтому здесь вместо реального петеринга используется совместимая заглушка TestOperationalSupport без изменения других компонентов.
* [ZookeeperTest](https://github.com/YandexClassifieds/baker/blob/5a7d42c35e2ea369fed3e01490cd5a561d416697/src/test/scala/ru/yandex/vertis/baker/ZookeeperTest.scala): пример использования ZookeeperNode.

## Типичный baker-сервис.

## Что такое компонент.

## Описание готовых компонентов.

## Описание прочих полезных штук.

----

Описать фишку с `trait MySqlMdbAwareImpl extends MySqlAware {`
