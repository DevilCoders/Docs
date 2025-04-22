### Мониторинги представлений в billing-tms
Схема:
![alt Моники: логика работы](../../_assets/images/architecture/moniks-thread-doc.jpg)

#### Описание алгоритма:
1. На машинке крутятся треды, которые ходят в таблицу `market_billing.monitor_query_result`
2. В таблице с локом выбирается самая старая запись у которой поле `task_status` не `PROCESSING` и она выполнялась в последний раз раньше чем ее `period`.
3. Тред обновляет `task_status` на `PROCESSING` и `last_run` на `current_timestamp`.
4. Тред начинает выполнение запроса выбранного мониторинга.
5. Если запрос выполнено успешно, то таблица обновляется на результаты запроса и `task_status`=`PENDING`
6. Если в ходе запроса была ошибка, то она записывается в таблицу и `task_status`=`ERROR`

#### Прочее
* Если моник зависает и выполняется очень долго, то ему проставляется `task_status`=`TIMEOUT`. См. [ViewMonitorTimeoutSetterExecutor](../../reference/jobs/list/viewMonitorTimeoutSetterExecutor.md)
* Результаты выполнения собираются раз в 10 минут и отправляются в juggler. См.  [ExportViewsMonitorToJugglerExecutor](../../reference/jobs/list/exportViewsMonitorToJugglerExecutor.md)

### Полезные ссылки
1. [ViewMonitoringsWorker](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/ViewMonitoringsWorker.java?#L21) - класс треда.
2. [JugglerMonitoringDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/JugglerMonitoringDao.java?#L43) - дао для работы с мониками. Написано на [JOOQ](../../guide/dev/jooq-quickstart.md).
3. [ViewMonitoringUpsertDbExecutor](../../reference/jobs/list/viewMonitoringUpsertDbExecutor.md) - дока cинхронизации моников в базе и в классе [MonitorItems](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java?#L16).
