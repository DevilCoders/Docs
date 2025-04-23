### Как добавить новую очередь /тип задачи
* Payload
`extends TraceableExecutionQueuePayload`

проверить, что десериализуется

Зажигаем мониторинг в случае FAIL-а задачи
* Producer
`extends BaseQueueProducer`

* Consumer
`extends BaseQueueConsumer`
  
### Состояние очереди
1. см. в БД `queue_task`. Если пусто, то задач нет
2. лог исполнения задач в БД `queue_log`
3. мониторинг
4. лог 
```
INFO  QueueRegistry: registered consumer: config={location={id=CANCEL_ORDER,table=queue_tasks}, settings={threadCount=1, betweenTaskTimeout=PT1M, noTaskTimeout=PT1M, processingMode=SEPARATE_TRANSACTIONS, retryType=GEOMETRIC_BACKOFF, retryInterval=PT1M, fatalCrashTimeout=PT1S}}
INFO  QueueExecutionPool: starting queues
INFO  QueueExecutionPool: running queue: queueId=CANCEL_ORDER, shardId=CANCEL_ORDER
INFO  QueueExecutionPool: created queue thread: threadName=queue-0-0, location={id=CANCEL_ORDER,table=queue_tasks}, shardId=CANCEL_ORDER

INFO BaseQueueProducer  : Producing queue entry with payload ru.yandex.market.tpl.core.domain.sc.cancel_order.CancelOrderPayload@1da8d860 for queue CANCEL_ORDER.
INFO BaseQueueProducer  : Successfully added new queue item with id 1 into queue CANCEL_ORDER.

INFO [queue-0-0] LoggingTaskListener : Task picked, queue=CANCEL_ORDER, task={...}, pickTaskTime=41
INFO [queue-0-0] LoggingTaskListener : Task started, queue=CANCEL_ORDER, task={...}
INFO [queue-0-0] BaseQueueConsumer   : Executing task {...} on queue CANCEL_ORDER

INFO [queue-0-0] BaseQueueConsumer   : Task {...} has been successfully processed
INFO [queue-0-0] LoggingTaskListener : Task executed, queue=CANCEL_ORDER, task={..., result={actionType=FINISH}, processTaskTime=12515}
INFO [queue-0-0] LoggingTaskListener : Task finished, queue=CANCEL_ORDER, task={...}

```
