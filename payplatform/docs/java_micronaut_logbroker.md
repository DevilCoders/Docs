# Библиотека micronaut-logbroker

Данная библиотека представляет собой интеграцию `logbroker` и `micronaut`. Из коробки поддерживается:

- Запись в сконфигурированные топики
- Чтение сообщений из сконфигурированных топиков
- Сериализация/десериализация сообщений в/из сырых данных
- Автоматическое восстановление в случае проблем

## Авторизация

На данный момент поддерживается следующие схемы авторизации:

- Без авторизации
- OAuth
- TVM2

### OAuth

Для авторизации при помощи `OAuth` необходимо предоставить токен пользователя от чьего имени будет происходить взаимодействие. Конфигурация осуществляется отдельно для `producer`'ов и `consumer`'ов (подробности см. ниже). Также из коробки предоставляется автоматический поиск токена если он не задан в конфиге. Механизм поиска осуществляется в следующем порядке:

1. Проверяется соответствующая секция конфига
2. Проверяется значение `environment variable` `LOGBROKER_TOKEN`, которая должна содержать путь к файлу с токеном
3. Проверяется наличие файла в `%HOME%/.logbroker/token`, который должен содержать токен

Если ни на одном из шагов токен не был найден, то инициализация завершается с ошибкой.

### TVM2

Для использования `tvm` авторизации необходимо предварительно сконфигурировать [micronaut-tvm](java_tvm.md) модуль, а также сконфигурировать `producer` или `consumer` выставив свойство `credentials` в значение `tvm`.

{% note warning %}

Важно не забыть прописать [tvm id](https://logbroker.yandex-team.ru/docs/concepts/security#tvm) используемых инсталляций `logbroker` в конфигурации `tvmtool` (для `Y.Deploy` это делается в конфиге соответствующего stage). При этом в конфиге приложения (секция `tvm2.services`) эти `tvm id` указывать не нужно, т.к. библиотека сделает это автоматически.

{% endnote %}

## Конфигурация кластеров logbroker

`logbroker` представлен несколькими [инсталляциями](https://logbroker.yandex-team.ru/docs/concepts/clusters_and_installations). Для начала работы нужно сконфигурировать кластеры под нужные инсталляции в конфиге:

```yaml
logbroker:
  cluster:
    main: # Задаем имя кластера по которому можно будет на него сослаться
      enabled: true
      installation: logbroker # Выбираем инсталляцию из значений перечисления LogbrokerInstallation
      balancer-terminate-timeout: 10s # Задаем таймаут на остановку машинерии из logbroker SDK
    ...
    clusterN:
      ....
```

## Запись сообщений

Чтобы записать сообщения в топик необходимо сконфигурировать producer. Подробности о том как производится запись в logbroker можно посмотреть [тут](https://logbroker.yandex-team.ru/docs/concepts/data/write).

```yaml
logbroker:
  producer:
    main: # Имя producer'а по которому будет доступен bean
      enabled: true
      cluster: main # Имя кластера для подключения producer
      topic: mytopic # Имя топика, в который будем писать
      source-id: 0 # Идентификатор группы сообщений в которую производится запись
      codec: raw # Кодек для данных сообщений. Ожидается одно из значений перечисления CompressionCodec
      group: 1 # Номер группы партиций
      dc: vla # (опционально) Задает ДЦ в который producer будет писать сообщения (подробности в секции 'Выбор ДЦ')
      credentials: oauth # Параметры авторизации.
      oauth-token: ... # (опционально) Используется только совместно с credentials=oauth, позволяет явно задать OAuth-токен
      extra-metadata: # Здесь можно задать произвольный набор пар ключ-значение, которые будут добавлены в метаданные каждого сообщения
        custom-key: 42
```

{% note tip %}

Подробности про группы сообщений можно посмотреть [тут](https://logbroker.yandex-team.ru/docs/concepts/resource_model#message-group).
Подробности про группы партиций можно посмотреть [тут](https://logbroker.yandex-team.ru/docs/concepts/resource_model#partition-group).

{% endnote %}

Далее в коде необходимо получить бин `producer`'а:

```java
import javax.inject.Inject;
import com.fasterxml.jackson.annotation.JsonCreator;
import io.micronaut.core.annotation.Introspected;
import lombok.Value;
import ru.yandex.payments.micronaut_logbroker.annotations.LogbrokerProducer;
import ru.yandex.payments.micronaut_logbroker.producer.Producer;

@Value
@Introspected
class MyMessage {
    private final String msg;
    private final int code;

    @JsonCreator
    MyMessage(String msg, int code) {
        this.msg = msg;
        this.code = code;
    }
}

class MyBean {
    private final Producer<MyMessage> producer;

    @Inject
    public MyBean(@LogbrokerProducer("main") // Задаем имя producer'а, описанного в конфиге
                  Producer<MyMessage> producer) {
        this.producer = producer;
    }

    public void foo() {
        producer.write(new MyMessage("msg", 42)); // можно писать java-объекты
        producer.write(new byte[] {0xDE, 0xAD, 0xBE, 0xEF}); // или сырые данные
    }
}
```

Отправка `ack` для записанных сообщений производится автоматически.

### Восстановление producer при ошибках

В случае возникновения ошибок записи происходит автоматическое пере подключение `producer`'а.

## Чтение сообщений

Для чтения сообщений необходимо сконфигурировать один или несколько читателей. Подробности о чтении данных из `logbroker` можно почитать [тут](https://logbroker.yandex-team.ru/docs/concepts/data/read).

```yaml
logbroker:
  consumer:
    consumer-name:
      cluster: main # Имя кластера для подключения consumer
      executor: io # executor на котором будет запускаться обработчик
      dc: vla # (опционально) Задает ДЦ из которого consumer будет читать сообщения (подробности в секции 'Выбор ДЦ')
      credentials: oauth # Параметры авторизации.
      oauth-token: ... # (опционально) Используется только совместно с credentials=oauth, позволяет явно задать OAuth-токен
      enabled: true
      client-id: logbroker-consumer # имя consumer в logbroker
      retries: # Параметры переподключения consumer'а
        enabled: true
        delay: 10s # Задержка между попытка переподключения
        restart-on-error: true # Выполнять переподключения в случае ошибки или нет
      committer:
        max-uncommitted-reads: 1 # Максимальное кол-во сообщений, которые могут быть прочитаны после последнего закомиченного
      reader:
        max-inflight-reads: 10
        max-unconsumed-reads: 1
      session:
        read-only-local: false # режим чтения зеркалированных топиков. true означает чтение только исходных топиков, без зеркалированных, false — чтение как исходных, так и зеркалированных топиков
        client-side-locks-allowed: false # режим присвоения партиций. true означает, что партиции будут присваиваться явно. false означает, что партиции будут присваиваться сервером автоматически
        force-balance-partitions: true # режим перераспределения партиций после инициализации текущей сессии. true означает, что сервер перераспределит партиции сразу же, не дожидаясь подтверждения чтения от других сессий. false означает, что сервер дождётся подтверждения чтения от других сессий до присвоения партиций текущей сессии
        commits-disabled: false # режим чтения без подтверждения прочтения true означает, что клиент может не подтверждать прочтение сообщений. Режим без подтверждения прочтения упрощает клиентскую логику, когда клиенту достаточно читать только актуальные сообщения с использованием параметра max_time_lag_ms
        groups: [ # список групп партиций топика, из которого будут выбраны партиции для присвоения клиенту. По умолчанию присваиваются все партиции. В большинстве случаев отсутствует необходимость использовать данный параметр
            1
        ]
        idle-timeout: 1m # время в течение которого соединение с logbroker будет активно в случае отсутствия сообщений
        max-read-messages-count: 1 # ограничение максимального количества сообщений в результате чтения
        max-read-size: 5mb # ограничение максимального размера результата чтения
        max-read-partitions-count: 0 # ограничение максимального количества партиций в результате чтения
```

Далее необходимо объявить обработчик сообщений:

```java
import com.fasterxml.jackson.annotation.JsonCreator;
import io.micronaut.core.annotation.Introspected;
import lombok.Value;
import reactor.core.publisher.Mono;
import ru.yandex.payments.micronaut_logbroker.annotations.LogbrokerListener;
import ru.yandex.payments.micronaut_logbroker.annotations.OffsetStrategy;
import ru.yandex.payments.micronaut_logbroker.annotations.Topic;
import ru.yandex.payments.micronaut_logbroker.consumer.Committer;
import ru.yandex.payments.micronaut_logbroker.consumer.ConsumerRecord;

@Value
@Introspected
class MyMessage {
    private final String msg;
    private final int code;

    @JsonCreator
    MyMessage(String msg, int code) {
        this.msg = msg;
        this.code = code;
    }
}

@LogbrokerListener(
    consumerId = "consumer-name", // имя одного из consumer'ов, описанных в конфиге
    strategy = OffsetStrategy.DISABLED
)
class MyConsumer {
    @Topic({"topicN", "topic100500"}) // задаем список топиков, которые будут обработаны данным методом
    public Mono<Void> consume(ConsumerRecord<MyMessage> record) {
        return Mono.empty();
    }

    @Topic("topicN")
    public void consume(ConsumerRecord<byte[]> record, Committer committer) {
        committer.commitSync();
    }
}
```

Параметр `strategy` позволяет задать одну из стратегий коммита:

- `ASYNC` - после завершения обработчика будет выполнен коммит, а обработка следующего `record`'а запуститься не дожидаясь подтверждения коммита от сервера
- `SYNC` - обработка следующего `record`'а начнется только после подтверждения предыдущего коммита сервером
- `MANUAL` - коммит будет выполнен пользователем при помощи аргумента типа `Committer`

{% note alert %}

Если один из обработчиков принимает аргумент типа `Committer`, то параметр `strategy` игнорируется и устанавливается в `MANUAL`.

{% endnote %}

`ConsumerRecord<T>` содержит батч десериализованных сообщений заданного типа `T`. Помимо этого для каждого сообщения доступна вся метаинформация: offset, timestamp, partition и т.д.

Возможные возвращаемые значения обработчиков:

- Любой реактивный тип (Mono, Publisher, etc): выполнение обработчика блокируется только в случае `strategy = SYNC`
- Наследники `CompletionStage`: аналогично реактивным типам
- Все остальные типы: обработка каждого `record` блокируется

### Валидация сообщений

Для входящих сообщений можно настроить применение `micronaut` валидации. Для этого необходимо добавить аннотацию `@Valid` на аргумент типа `ConsumerRecord` и разметить тип сообщения аннотациями из пакета `javax.validation`. После этого каждое входящее сообщение будет провалидировано и, в случае несоответствия значения требованиям, обработка сообщения будет завершаться ошибкой `ConstraintViolationException`, которая будет передана в `LogbrokerListenerExceptionHandler`.

### Обработка ошибок

Для обработки ошибок можно определить бин, унаследованный от интерфейса `LogbrokerListenerExceptionHandler`, который будет вызываться на каждую ошибку. Обработчик по-умолчанию просто логирует все ошибки.

### Восстановление consumer при ошибках

Стратегия восстановления задается в конфиге `logbroker.consumer.*.retries`.

## Сериализация/десериализация сообщений

Для сериализации/десериализации сообщений используются реализации интерфейса `Serde` для конкретного типа. Из коробки предоставляются реализации `Serde` для `String`, `byte[]` и `json`/`tskv` сериализация/десериализация `@Introspected` классов.

Для использования `tskv` `Serde` для `@Introspected` класса необходимо пометить его аннотацией `@Tskv`.

## Выбор ДЦ

По-умолчанию библиотека перекладывает выбор ДЦ на `logbroker`, используя общий хост балансера кластера. Такой подход может привести к невозможности прочитать сообщения (например, если для `producer`'а будет выбран один ДЦ, а для `consumer`'а, использующего `read rule type = all-original`, другой).

Для `producer` и `consumer` доступна возможность задать желаемый ДЦ в параметрах, указав одно из значений перечисления `PreferredDC`:

- `vla` - Владимир
- `sas` - Сасово
- `man` - Мянтсяля
- `myt` - Мытищи
- `iva` - Ивантеевка
- `local` - Локальный ДЦ, в котором запущено приложение. Определение ДЦ производится посредством `CloudMetadataProvider` из [utils](java_utils.md). В случае невозможности определения локального ДЦ конфигурация завершится с ошибкой, это необходимо учитывать при написании тестов.
