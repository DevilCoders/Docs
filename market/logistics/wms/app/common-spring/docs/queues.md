# Сервис очередей

Сервис доставки очередей поддерживает три брокера:
* RabbitMQ
* SQS-совместимые сервисы (Yandex Messaging Service)
* embedded (ActiveMQ Artemis)

Поддержка ActiveMQ добавлена для локальной разработки, чтобы не требовалось поднимать тяжелые брокеры.
Для брокеров RabbitMQ и SQS поддерживается доставка сообщений с ретраями.


## Интеграция в сервис

Для работы с очередями требуется настройка:

1. загрузить конфигурацию `ru.yandex.market.wms.shared.libs.async.configuration.CommonJmsConfiguration` и включить поддержку JMS аннотацией `@EnableJMS`.

```
@EnableJms //<===
@SpringBootApplication
@Import({
        CommonJmsConfiguration.class //<===
})
public class ServicebusApp {
```

2. в `application.yml` сервиса включить конфигурацию `application-fragment-mq.yml`:

```
spring:
  application.name: ...
  profiles:
    active: ...
  config:
    import:
      - application-fragment-mq.yml
```

3. если очередь нужна также для тестов, то в тестовом `application.yml` нужно включить конфигурацию `application-fragment-mq-test.yml`:

```
spring:
  application.name: ...
  profiles:
    active: ...
  config:
    include:
      - application-fragment-mq-test.yml
```

4. (для SQS) создать необходимые бины для интеграции с TVM (если они еще не создаются) и добавить ID SQS в список сервисов, с которыми работает ваш сервис, в настройки клиента TVM.
   В качестве примера можно использовать класс `ru.yandex.market.wms.servicebus.configuration.TvmConfiguration`:

```
    @Bean
    @Profile({Profiles.PRODUCTION, Profiles.TESTING})
    public TvmClient tvmClient() {
        TvmApiSettings tvmApiSettings = new TvmApiSettings()
                .setSelfTvmId(servicebusTvmServiceId)
                .enableServiceTicketsFetchOptions(
                        servicebusTvmSecret,
                        new int[] {
                                transportationTvmServiceId,
                                irisTvmServiceId,
                                SqsJmsConfiguration.SQS_PRODUCTION_ID // <===
                        }
                ).enableServiceTicketChecking()
                .setDiskCacheDir(cacheTvmDir);

        return new NativeTvmClient(tvmApiSettings);
    }
```

5. (для SQS) выдать права для работы нового сервиса ([настройка AWS CLI](https://wiki.yandex-team.ru/sqs/#cli)) для учетных записей "wms-dev", "wms-test", "wms":

```
aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions --path <учетная запись> --subject <ID сервиса>@tvm --permissions AlterQueue CreateQueue DeleteMessage DescribePath ReceiveMessage SendMessage
```

Для отправки сообщений использовать `JmsTemplate` из контекста Spring и post-обработчик `ru.yandex.market.wms.shared.libs.async.jms.RetryableMessagePostProcessor`

```
@Service
@AllArgsConstructor
@Slf4j
public class SomeAsyncService {
    private static final String QUEUE_NAME_TPL = DestNamingUtils.WAREHOUSE_QUEUE_PREFIX + "queueName";

    private final JmsTemplate defaultJmsTemplate;

    // послать в очередь
    public void sendDimensions(ObjectDTO payload) {
        defaultJmsTemplate.convertAndSend(QUEUE_NAME_TPL, payload, RetryableMessagePostProcessor::apply);
    }
```

Для получения сообщений в дополнение к аннотации `@JmsListener` нужно использовать аннотацию `@ru.yandex.market.wms.shared.libs.async.jms.Retry`.
Также у метода должен быть параметр, аннотированный `@Payload`, и параметр с типом `MessageHeaders`.

```
@Service
@AllArgsConstructor
@Slf4j
public class SomeAsyncService {
    private static final String QUEUE_NAME_TPL = DestNamingUtils.WAREHOUSE_QUEUE_PREFIX + "queueName";

    // получить из очереди
    @JmsListener(destination = QUEUE_NAME_TPL)
    @Retry
    public void receiveDimensions(@Payload ObjectDTO payload, MessageHeaders headers) {
        //process
    }
}
```

Важно, чтобы имена очередей начинались со специального префикса, который задан в константе `DestNamingUtils.WAREHOUSE_QUEUE_PREFIX`.

Тип сервиса задается настройкой ```MqProvider=rabbitmq|sqs|embedded``` в properties-файле стенда.

## Работа с сообщениями в DLQ

Если сообщение не удалось обработать за заданное число попыток, то оно перемещается в DLQ.

Для повторной обработки данных сообщений нужно дёрнуть ручку `/serviceus/reanimateDeadQueue/<queue_name>?cnt=1`:
* в `queue_name` задается имя очереди, в которую нужно вернуть сообщения
* параметр `cnt` не является обязательным и ограничивает максимальное количество сообщений для восстановления


## Настройка

### RabbitMq

В файле настроек стенда нужно задать следующие параметры:

```
MqProvider=rabbitmq
RabbitMqAddresses=amqp://host1:port1,amqp://host2:port2,...
RabbitMqManagementAddresses=https://host1:port1,https://host2:port2,...
RabbitMqUser=<пользователь>
RabbitMqPass=<пароль>
```


### SQS

В файле настроек стенда нужно задать следующие параметры:

```
MqProvider=sqs
SqsEndpoint=<endpoint>
SqsRegion=<регион>
SqsUser=<пользователь>
```

Для разработки можно использовать пользователя `wms-dev`.

### Embedded (ActiveMQ Artemis)

В файле настроек стенда нужно задать следующие параметры:

```
MqProvider=embedded
```


## Принцип работы

Ниже описан принцип поддержки ретраев обработки сообщений из очереди для RabbitMQ.

![Принцип повторной обработки сообщений в RabbitMQ](images/retry-mechanism-rabbitmq.png)

1. Отправка сообщения в processing-очередь.
2. Чтение сообщения из очереди слушателем.
3. Отправка сообщения на повторное выполнение в delay-очередь с TTL для сообщений. Для delay-очередей с TTL задана
   очередь DLQ, куда отправляются сообщения после достижения TTL. Наименование очереди содержит значение TTL,
   например: `rmq_0_ttl5_delay`. При каждой отправке на повторное выполнение у сообщения увеличивается счетчик в
   заголовке, отмечающий количество попыток обработки.
4. Отправка сообщения в delay-очередь. Пример наименования delay-очереди: `rmq_0_delay`.
5. Чтение сообщения слушателем для последующего перекладывания в processing-очередь.
6. Отправка сообщения в processing-очередь.
7. Отправка сообщения на повторное выполнение в delay-очередь с TTL для сообщений.
8. Отправка сообщения в delay-очередь.
9. Отправка сообщения на повторное выполнение в delay-очередь с TTL для сообщений.
10. Отправка сообщения в delay-очередь.
11. Если сообщение не удалось обработать за заданное число попыток, то оно перемещается в dead-очередь.
    Пример наименования dead-очереди: `rmq_0_dead`. Сообщения в данной очереди автоматически не обрабатываются.
12. Можно также сделать, чтобы сообщение попадало в dead-очередь с TTL. Для этого для отправки на повторное выполнение
    нужно вызвать метод `JmsRetry#retryWithTtlForDeadQueue`.

Для SQS принцип работы немного другой.

![Принцип повторной обработки сообщений в SQS](images/retry-mechanism-sqs.png)

1. Отправка сообщения в processing-очередь.
2. Чтение сообщения из очереди слушателем.
3. Отправка сообщения на повторное выполнение в delay-очередь. Сообщение отправляется с параметром delivery delay.
   При каждом повторе это значение увеличивается экспоненциально. Пример наименования delay-очереди: `rmq_0_delay`.
   При каждой отправке на повторное выполнение у сообщения увеличивается счетчик в
   заголовке, отмечающий количество попыток обработки.
4. Когда пройдет время, переданное в delivery delay, сообщение становится видимым в delay-очереди.
   После этого его прочитает слушатель для последующего перекладывания в processing-очередь.
5. Отправка сообщения в processing-очередь.
6. При достижении лимита повторного выполнения, сообщение направляется в dead-очередь.
   Пример наименования dead-очереди: `rmq_0_dead`. Сообщения в данной очереди автоматически не обрабатываются.
7. Можно также сделать, чтобы сообщение попадало в dead-очередь с TTL. Для этого для отправки на повторное выполнение
   нужно вызвать метод `JmsRetry#retryWithTtlForDeadQueue`.
