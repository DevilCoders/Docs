### Как использовать?

Если достаточно читать в один поток:
```java
@EnableEventsConsumer
public class EventsConsumerConfiguration {
    @Bean(name="eventsConsumer")
    public Consumer<List<OrderHistoryEvent>> eventsConsumer() {
        return events -> {};
    }
    
    @Bean(name="lbReaderOffsetDao")
    public SimpleJdbcLbReaderOffsetDao simpleJdbcLbReaderOffsetDao(JdbcTemplate jdbcTemplate) {
        return new SimpleJdbcLbReaderOffsetDao(jdbcTemplate);
    }
}
```
Если нужно читать в несколько потоков:
```java
@EnableEventsConsumer(consumerCount = 3)
@Configuration
@ImportResource("classpath:WEB-INF/checkouter-serialization.xml")
public static class TestConfiguration {
    @Bean(name = "eventsConsumerFactory")
    public ConsumerFactory<List<OrderHistoryEvent>> eventsConsumer() {
        return (i) -> (events) -> {
        };
    }
    
    @Bean(name="lbReaderOffsetDao")
    public SimpleJdbcLbReaderOffsetDao simpleJdbcLbReaderOffsetDao(JdbcTemplate jdbcTemplate) {
        return new SimpleJdbcLbReaderOffsetDao(jdbcTemplate);
    }
}
```


Перемапить проперти:
```properties
# Список логброкерных клиентов.
market.checkout.logbroker.consumer.clients=${market.personal_data_collector.logbroker.consumer.clients}
# tvm id потребителя
market.checkout.logbroker.consumer.src.client_id=${market.personal_data_collector.logbroker.src.client_id:0}
# tvm secret потребителя
market.checkout.logbroker.consumer.src.client_secret=${market.personal_data_collector.logbroker.src.client_secret:}
# tvm secret логброкера
market.checkout.logbroker.consumer.tvmClientId=${market.personal_data_collector.logbroker.dst.client_id:0}
# стратегия обработки исключений
market.checkout.logbroker.consumer.exception_strategy=SWALLOW_EXCEPTIONS
```

Также в контексте ожидаются следующие бины (не будут зарегистрированы автоматически):
1. transactionTemplate (org.springframework.transaction.support.TransactionTemplate)
2. checkouterAnnotationObjectMapper (com.fasterxml.jackson.databind.ObjectMapper) - можно заимпортить из classpath:WEB-INF/checkouter-serialization.xml

