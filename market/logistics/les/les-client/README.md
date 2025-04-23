# Как подключиться к SQS и использовать клиент

- Основная документация по подключению [тут](https://wiki.yandex-team.ru/delivery/development/apps/agregator-logisticheskix-sobytijj/integration/)

1. Доступ в [puncher](https://puncher.yandex-team.ru) для своего сервиса к `sqs.yandex.net`, порт `8771`. В комментариях укажите, что нужно подлючения
   к очередям сервиса
   [**Агрегации логистических событий**](https://abc.yandex-team.ru/services/logistics_event_service/)
   и аккаунтам `logistics-event-service-ymq-testing` `logistics-event-service-ymq-stable`
2. Конфигурация подключения:

```properties
sqs.region=eu-west-1
sqs.secretKey=unused
sqs.accessKey=logistics-event-service-ymq-stable #или testing
sqs.endpointHost=http://sqs.yandex.net:8771
sqs.connectionPoolSize=500
sqs.waitTimeSeconds=1
sqs.consumerConcurrency=1
sqs.visibilityTimeoutInSeconds=80
# Deprecated, use visibilityTimeoutInSeconds
sqs.visibilityTimeout=80
# LES CLIENT
# имя константы-проекта из енама ru.yandex.market.request.trace.Module
# нужно для правильной трассировки 
les.client.trace.producerProject=EXAMPLE_PROJECT
# трассировка sqs запросов в les
les.client.trace.enabled=true
```

При создании подписчика / источника через админку LES сам создает SQS-очередь.
Для создания очередей из кода можно использовать [SqsQueueService](https://a.yandex-team.ru/arc_vcs/market/logistics/les/les-app/src/main/kotlin/ru/yandex/market/logistics/les/service/SqsQueueService.kt?rev=r9393205#L13).

3. Если нужно читать из очереди, то необходимо создать consumer:

```kotlin
    @Service
    open class SqsEventConsumer(private val traceTskvLogger: SqsRequestTraceTskvLogger) {
        @JmsListener(destination = "queueName", containerFactory = "listenerContainerFactory")
        fun processEvent(
            @Header(JmsHeaders.DESTINATION) destination: SQSQueueDestination,
            @Header(JmsHeaders.MESSAGE_ID) messageId: String,
            @Header(TraceableMessagePostProcessor.PROPERTY_REQUEST_ID) requestId: String?,
            @Header(TraceableMessagePostProcessor.PROPERTY_TIMESTAMP) timestamp: Long?,
            event: Event
        ) {
           traceSqsLogger.logSqsRequestIn(
                requestId,
                requestTimestamp,
                mapOf("queue" to destination.queueName, "queueUrl" to destination.queueUrl, "messageId" to messageId)
           )
           
           // do some cool stuff
        }
    }
```

4. Добавить `tvm id` для работы с `SQS`. Можно использовать tvmId = 2002456 напрямую, либо использовать
   заготовленную [конфигурацию клиента](https://a.yandex-team.ru/projects/logistics_event_service/code/market/logistics/les/les-client/src/main/kotlin/ru/yandex/market/logistics/les/client/configuration/sqs/SqsTvmConfiguration.kt?dir=market%2Flogistics%2Fles)
   в виде бина `ExternalServiceProperties sqsServiceProperties`.

5. Получить права на работу с SQS:

```sh
aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions --path \
    logistics-event-service-ymq-{testing|stable} --subject {tvm_id}@tvm \
    --permissions CreateQueue DeleteQueue ReceiveMessage SendMessage AlterQueue DeleteMessage DescribePath
   
```

Для просмотра списка очередей можно настроить aws для тестинга и прода

```sh
#~/.aws/config
[default]
region = eu-west-1
output = json

[profile prod] # да, со словом profile 
region = eu-west-1

#~/.aws/credentials
[default]
aws_access_key_id=logistics-event-service-ymq-testing
aws_secret_access_key=unused
aws_session_token={SOMETOKEN}

[prod] # да, без слова profile
aws_access_key_id=logistics-event-service-ymq-stable
aws_secret_access_key=unused
aws_session_token={SOMETOKEN}
```

```sh
# и далее творим всякое
# для тестинга
aws ya-sqs --endpoint http://sqs.yandex.net:8771 list-queues
# для прода
aws --profile prod ya-sqs --endpoint http://sqs.yandex.net:8771 list-queues
# и так далее
```
