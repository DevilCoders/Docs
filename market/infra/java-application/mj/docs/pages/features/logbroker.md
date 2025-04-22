# Модуль Logbroker

## Особенности
- Модуль основан на библиотеке [market/jlibrary/logbroker-integration](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/logbroker-integration) и  
оффициальном SDK [kikimr/persqueue/sdk/java/v0](https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/persqueue/sdk/java/v0)
- Можно пользоваться всем что есть в этих библиотеках

## Конфигурирование
Проперти для конфигурирования задаются в `service.yaml`
Пример конфига:
```yaml
modules:
  logbroker:
    env:
      testing:
        installations:
          logbroker_prestable:
            - man
      production:
        installations:
          logbroker:
            - vla
            - sas
          lbkx:
            - lbkx
```
  Список доступных [инсталяций](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/logbroker-spring-boot-starter/src/main/java/models/LogbrokerInstallationType.java ) и [кластеров](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/logbroker-spring-boot-starter/src/main/java/models/LogbrokerClusterType.java)
  Если у инсталяций не указывать кластеры, то создадутся объекты для работы со всеми кластерами выбранной инсталяции.


Все параметры для настройки logbroker в `service.yaml`:
```yaml
modules:
  logbroker:
    env:
      testing:
        installations:
          logbroker_prestable:
            - man
      production:
        installations:
          logbroker:
            - vla
          lbkx:
        testOnReturn:
        maxWaitMillis:
        maxTotal:
        maxIdle:
        minIdle:
        maxRetries:
```
## Авторизация
Модуль поддерживает интеграцию с MJ модулем [tvm](tvm.md).
Если tvm для какого-то окружения не установлен, то используется OAuth токен.
Его можно передать через пропертю `mj.logbroker.oauth_token`

## Использование
Для работы с инсталяциями и кластерами нужно подтянуть бин `LogbrokerInstallations`
```java
@Autowired
LogbrokerInstallations logbrokerInstallations;
```

Получить необходимую инсталяцию(для работы с многокластерной инсталяцией) или кластер (для работы с одним кластером)
```java
LogbrokerInstallation installation = logbrokerInstallations.getInstallation(LogbrokerInstallationType.LOGBROKER);
LogbrokerCluster cluster = logbrokerInstallations.getCluster(LogbrokerClusterType.VLA);
```

Определить топик и имя консьюмера
```java
String topic = "logbroker-playground/pavellysenko/demo-topic";
String sourceId = "logbroker-playground/pavellysenko/demo-consumer";
```


### Писатели
```java
// создаем конфиг продьюссера
AsyncProducerConfig config = AsyncProducerConfig.defaultConfig(topic, sourceId.getBytes());
// поправить AsyncProducerConfig по необходимости
// создаем объект producer
AsyncProducer producer = cluster.createAsyncProducer(config);
// инициализация
producer.init().join();
// пишем в топик
producer.write("Hello world!".getBytes());
```

Есть возможность поспользоваться `LogbrokerEventPublisher`
Имплементация `LogbrokerEventPublisherImpl` использует `SimpleAsyncProducerProvider` (передаем ему `ProducerConfig` и `RetryOperations`)
и содержит основной метод `publishEventAsync` для публикации события.

`SimpleAsyncProducerProvider` имеет пул продьюссеров и выдает `SimpleAsyncProducer` по запросу через интерфейс `ProducerPoolObjectFactory` (реализации `PooledSimpleAsyncProducerObjectFactory` и `UniformlyDistributedProducerObjectFactory`)

интерфейс `SimpleAsyncProducer` расширяет `AsyncProducer`. Есть реализация  `PooledSimpleAsyncProducer` (и ее расширение `InvalidPooledAsyncProducer`)

Пул можно настривать промертями
```
mj.logbroker.testOnReturn
mj.logbroker.maxWaitMillis
mj.logbroker.maxTotal
mj.logbroker.maxIdle
mj.logbroker.minIdle
```

### Читатели
```java
// создаем конфиг читателя
StreamConsumerConfig consumerConfig = StreamConsumerConfig.defaultConfig(Collections.singleton(topic), sourceId);
// поправить StreamConsumerConfig по необходимости
// создаем объект consumer к нужному клсатеру (или инсталяции)
StreamConsumer consumer = cluster.createStreamConsumer(consumerConfig);
// запуск читателя
consumer.startConsume(listener);
```
listener это объект класса `StreamListener`
Нужно создать имплементацию интерфейса `StreamListener`, для обработки входящих сообщений.
Подробнее можно прочитать в [документации sdk logbroker](https://logbroker.yandex-team.ru/docs/how_to/develop_with_java_2#asinhronnoe-chtenie).

Еще пример из [здоровья](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-health/logshatter/src/main/java/ru/yandex/market/logshatter/reader/logbroker/topic/LbTopicReaderService.java?rev=r8987109#L234)

Можно использовать [TransactionalLogbrokerListener](https://a.yandex-team.ru/arc_vcs/market/logistics/iris/iris-app/src/main/java/ru/yandex/market/logistics/iris/service/logbroker/consumer/TransactionalLogbrokerListener.java) (уже подключен к стартеру).
Его можно создать через `TransactionalLogbrokerListenerFactory`, передав имплементацию обработчика сообщений `LogbrokerDataProcessor reader`
Настроить ретраи `TransactionalLogbrokerListener` (для бина `logbrokerServiceRetryTemplate`) можно через пропертю `mj.logbroker.maxRetries` (по умолчанию 5)

#### Кастомные экзекьютеры
На каждый кластер можно назначить свой кастомный экзекьютор
```java
@Bean
public NamedExecutorService createExecutorService() {
    ThreadFactory threadFactory = new ThreadFactoryBuilder()
        .setDaemon(true)
        .setNameFormat("custom_name_%s")
        .build();
    return new NamedExecutorService(LogbrokerClusterType.VLA, Executors.newCachedThreadPool(threadFactory));
}
```

## Обработка ошибок при чтении
Во время чтения могут возникать необрабатываемые исключения.
Исключения из метода `onRead` не пробрасываются дальше и просто игнорируются.
Поэтому, коммита не происходит, а сообщение теряется. 

Консьюмер продолжает получать и обрабатывать собщения, но уже не может сделать коммит в логброкер, т.к. если одно из предыдущих сообщений не закомиченно, последующие тоже не комитятся.  
Т.е. обработка происходит зря, и при перебалансировке или разрыве соединения чтение опять начнется с первого не закомиченного сообщения.

Для решения этой проблемы есть несколько вариантов решения. Все они доступны и не в mj сервисе.

### 1. Метод onUncaughtException
Для обработки ошибок в `StreamListener` есть метод `onUncaughtException`,
который вызывается при [выбрасывании](https://a.yandex-team.ru/arcadia/kikimr/persqueue/sdk/java/v0/src/main/java/ru/yandex/kikimr/persqueue/consumer/stream/AbstractStreamConsumer.java?rev=r9358901#L101)
 исключения из метода `onRead`.
Его так же можно переопределить в своей имплементации `StreamListener`.

### 2. Консьюмер с реконнектами 
Может быть полезным кастомизировать конфигурацию consumer.
Например, можно настроить рестарт консьюмера при закрытии сессии или ошибке,
пришедшей от логброкера или возникшей во время обработки сообщения.
Это можно сделать через `RetryConfig`, который является частью `StreamConsumerConfig`:
```java
StreamConsumerConfig consumerConfig = StreamConsumerConfig.defaultConfig(Collections.singleton(topic), sourceId)
        .toBuilder()
        .configureRetries(r -> r.enable().setShouldRestartOnClose(() -> false).setShouldRestartOnUncaughtError(() -> true))
        .build();
```
При выставлении флага `shouldRestartOnUncaughtError` и получении необработанной ошибки при чтении,
консьюмер сначала выполнит метод `onUncaughtException` из `Listener`, а затем произойдет реконнект
 и чтение начнется с незакомиченного сообщения.
Таймаут между остановкой и началом чтения можно задать используя 
[RetryPolicy из RetryConfig](https://a.yandex-team.ru/arcadia/kikimr/persqueue/sdk/java/v0/src/main/java/ru/yandex/kikimr/persqueue/consumer/stream/retry/RetryConfig.java?rev=r9358901#L14)
Это нужно для того, что бы не продолжать чтение и обработку без коммита в логброкер.

### 3. Dead letter queue (DLQ)

Бывают ошибки при чтении, когда сообщение неправильное (бинарник или протобаф неправильный), 
или когда во время чтения не смогли записать результат в базу или еще куда-то сходить.
Что делать с недообработанными\неправильными сообщениями?
* просто откинуть
* остановить чтение из данной партиции
* механизм DLQ. Т.е. записывать сообщение в специальное место для последующей обработки. 
Таким местом может быть, например, топик или база данных.

Мы реализовали этот механизм в специальной библиотеке [market/jlibrary/logbroker-dlq](https://a.yandex-team.ru/arcadia/market/jlibrary/logbroker-dlq).

#### Как воспользоваться?

Нужно воспользоваться специальной оберткой над существующим объектом listener.
([DlqListener](https://a.yandex-team.ru/arc_vcs/market/jlibrary/logbroker-dlq/src/main/java/ru/yandex/market/logbroker/dlq/DlqListener.java?rev=r9691174#L35) и его реализации [DlqBatchingStreamListener](https://a.yandex-team.ru/arc_vcs/market/jlibrary/logbroker-dlq/src/main/java/ru/yandex/market/logbroker/dlq/DlqBatchingStreamListener.java?rev=r9691174#L10)и [DlqStreamListener](https://a.yandex-team.ru/arc_vcs/market/jlibrary/logbroker-dlq/src/main/java/ru/yandex/market/logbroker/dlq/DlqStreamListener.java?rev=r9691174#L9))

```java
consumer.startConsume(new DlqStreamListener(originalListener, consumer, dlqHandler, strategyProvider, monitoringService));
```
здесь
* ``originalListener`` - основной listener, который реализует интерфейс StreamListener.
* ``consumer`` - консьюмер, которому хотим добавить логику dlq. Необходимо передать для остановки нужного консьюмера в случае ошибки.
* ``dlqHandler`` - объект, который определяет место хранения необработанных сообщений.
    Это может быть ``TopicDlqHandler``, ``PostgresDlqHandler`` или ваш собственный объект реализующий интерфейс ``DlqHandler``.
* ``strategyProvider`` - функция, которая получает поломанное сообщение и ошибку и возвращает стратегию обработки этого сообщения.
    например ```(ConsumerReadResponse r, Exception e) -> ExceptionStrategy.SAVE```. Не обязательный аргумент, по умолчанию ExceptionStrategy.SAVE.
* ``monitoringService`` - [MonitoringService](https://a.yandex-team.ru/arc_vcs/market/jlibrary/logbroker-dlq/src/main/java/ru/yandex/market/logbroker/dlq/monitoring/MonitoringService.java?rev=r9691174#L5). 
Для активации мониторингов при сохранении в dlq/пропуске события/остановке чтения. Не обязательный аргумент, по умолчанию пустой и ничего не делает.

{% note info %}

В случае, если во время сохранения в dlq, возникает ошибка, консьюмер останавливается.

{% endnote %}


Ниже описаны реализованные в библиотеке [market/jlibrary/logbroker-dlq](https://a.yandex-team.ru/arcadia/market/jlibrary/logbroker-dlq) DlqHandler'ы с сохранением в базу и в топик

#### Сохранение в топик. TopicDlqHandler
В основе `TopicDlqHandler` лежит `LogbrokerEventPublisher`.
Внутри Publisher содержит пул продьюссеров. Каждый батч от логброкера обрабатывается в отдельном потоке. 
При возниконовении ошибки в нескольких потоках, каждый из них возьмет из пула своего продьюсеера и запишет сообщение в dlq топик.

Для создания объекта потребуется: имя топика для записи, хост логброкера, параметры аутентификации:
```java
new TopicDlqHandler(dlqTopicName, dlqCluster);
```
* `dlqTopicName` - строка, где указан топик, куда будут складываться необработанные сообщения.
* `dlqCluster` - кластер логброкера, в который будем писать.

при работе без mj можно воспользоваться другим конструктором
```java
new TopicDlqHandler(
        "logbroker-playground/staff_login/dlq-topic",
        "vla.logbroker.yandex.net",
        () -> Credentials.oauth(oauthToken));
```

При возникновении ошибки при записи можно настроить ретраи, для этого нужно передать объект RetryOperations.
Для более тонкой настройки пула продьюссеров можно воспользоваться ProducerConfig. 
Для добавления какой-либо дополнительной информации в записываемое сообщение есть [LogbrokerEventFactory](https://a.yandex-team.ru/arc_vcs/market/jlibrary/logbroker-dlq/src/main/java/ru/yandex/market/logbroker/dlq/handler/topic/LogbrokerEventFactory.java?rev=r9691174#L6).
Подробнее можно ознакомится со всеми конструкторами [тут](https://a.yandex-team.ru/arc_vcs/market/jlibrary/logbroker-dlq/src/main/java/ru/yandex/market/logbroker/dlq/handler/topic/TopicDlqHandler.java?rev=r9691174#L63).

#### Сохранение в БД postgres. PostgresDlqHandler

Для создания объекта PostgresDlqHandler потребуется только DataSource.
```java
new PostgresDlqHandler(dataSource);
```
Рекомендуется использовать пул коннектов к базе (например hikari, который можно настроить в модуле postgres),
что бы не блокировать запись в базу.

Можно кастомизировать имя таблицы и настроить размер батча сообщений, записываемого в постгрес.
Подробнее [тут](https://a.yandex-team.ru/arc_vcs/market/jlibrary/logbroker-dlq/src/main/java/ru/yandex/market/logbroker/dlq/handler/postgres/PostgresDlqHandler.java?rev=r9691174#L70).

Сообщения будут сохранятся в таблицу согласно ее схеме.

{% cut "Схема таблицы в базе данных" %}

```sql
 create table saved_messages (
         id bigserial not null primary key,
         topic varchar(64) not null,
         message_partition bigint not null,
         message_offset bigint not null,
         source_id bytea not null,
         seq_no bigint not null,
         create_time_ms bigint,
         write_time_ms bigint,
         ip varchar(64),
         codec varchar(64),
         extra_fields jsonb,
         message_data bytea not null,
         exception_time timestamp without time zone default (now()) not null,
         exception_type text,
         exception_place text
        );
create index saved_messages_idx on saved_messages (topic, message_partition);
```

{% endcut %}

## Как попробовать читать и писать?
[quickstart](https://logbroker.yandex-team.ru/docs/quickstart)

## Стартер для сервисов без MJ
Стартер предназаначен для быстрого подключения **Logbroker** в любой проект на **Spring Boot**

### Установка
Добавить в `ya.make` зависимость:
```
market/infra/java-application/spring-boot-starters/logbroker-spring-boot-starter
```

### Конфигурировани
Для конфигурации инсталяциий можно указать список используемых кластеров в проперти mj.logbroker.installations.<имя инсталяции>.
Например,
```
mj.logbroker.installations.logbroker[0] = vla
mj.logbroker.installations.logbroker[1] = sas
mj.logbroker.installations.lbkx[0] = lbkx
```

### Авторизация
Авторизация просходит с помощью tvm. Если tvm для како-то окружения не установлен, то используется OAuth токен.
Его можно передать через пропертю `mj.logbroker.oauth_token`.
