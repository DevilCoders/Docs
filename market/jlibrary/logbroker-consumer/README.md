# idx-api-client
Клиент для доступа к http IDX API

### Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)

### Релизы в ЦУМе
[pipeline](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/logbroker-consumer-java-library), 
[dashboard](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/logbroker-consumer-java-library)


### Как использовать?

#### Настройка соединения с Logbroker

Нужно создать бин `LogbrokerConnetionParams` с параметрами подключения к Logbroker и источником tvm тикета.

Также нужно добавить LbReaderOffsetDao и иметь transactionTemplate в контексте.

```java
@Configuration
@EnableLogbrokerConsumer
public class ExampleConfiguration {
    
    @Bean
    @ConfigurationProperties("market.checkout.lbkx.balancer")
    public LogbrokerConnectionParams logbrokerConnectionParams(Tvm2 tvm2,
                                                               int logbrokerTvmId) {
        LogbrokerConnectionParams params = new LogbrokerConnectionParams();
        params.setCredentialsSupplier(
                        () -> Credentials.tvm(
                                tvm2.getServiceTicket(logbrokerTvmId)
                                        .getOrThrow("No tvm ticket for logbroker client")
                        )
                );
        return params;
    }
    
    @Bean
    public LbReaderOffsetDao simpleJdbcLbReaderOffsetDao(JdbcTemplate jdbcTemplate) {
        return new SimpleJdbcLbReaderOffsetDao(jdbcTemplate);
    }
}
```

#### Создание консумеров
Конфигурация непосредственно потребителей осуществляется путем добавления бинов `LogbrokerConsumerBuilder<?>` в контекст.

Если достаточно читать в один поток:

```java
@Configuration
@EnableLogbrokerConsumer
public class ExampleConfiguration {
    
    @Bean
    public LbParser<OrderHistoryEvent> parser() {
        return new EventsLbParser("dsd");
    }
    
    @Bean
    public Consumer<List<OrderHistoryEvent>> eventsConsumer() {
        return events -> {};
    }
    
    @Bean
    public LogbrokerConsumerBuilder<OrderHistoryEvent> logbrokerConsumerBuilder(
            LbParser<OrderHistoryEvent> parser) {
        return LogbrokerConsumers.single(
                "checkouter_order",
                "topic",
                "client/24",
                parser,
                eventsConsumer(),
                null
        );
    }
    
}
```
Если нужно читать в несколько потоков можно создать несколько `LogbrokerConsumerBuilder<?>` в контекст, 
либо написать свой или `LogbrokerConsumers.prefixed()`, который создаст по одному консумеру на каждого клиента, 
переданного ему на вход.
```java
@Configuration
@EnableLogbrokerConsumer
public class ExampleConfiguration {
    @Bean
    public LogbrokerConsumerBuilder<LocalDate> logbrokerConsumerBuilder(LbParserFactory<LocalDate> parserFactory,
                                                                        ConsumerFactory<LocalDate> consumerFactory) {
        return LogbrokerConsumers.prefixed(
                Arrays.asList("clients/12", "clients/25", "client/677"),
                "entity",
                "topic",
                parserFactory,
                consumerFactory
        );
    }
}
```

#### Получение консумеров

Все созданные консумеры реализуют интерфейс `LogbrokerReader` и помещаются в контекст, их можно получить с помощью `@Autowire`.

Также можно заинжектить бин `LogbrokerConsumerRegistry` и найти всех консумеров там.

### См. также

`/arcadia/market/checkout/checkouter-event-queue-client` - тут лежит парсер и готовая конфигурация для получения 
событий по заказам чекаутера. 