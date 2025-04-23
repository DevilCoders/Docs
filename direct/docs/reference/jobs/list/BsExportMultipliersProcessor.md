## BsExportMultipliersProcessor

### Продукт/подсистема

ESS транспорт в БК/CaeSaR.


### Роль в работе продукта/подсистемы

Отправляет корректировки в контент-систему БК, а скоро и в CaeSaR. Кроме корректировок из `hierarchical_multipliers` этим транспортом так же отправляются временной таргетинг кампаний - `campaigns.time_target` (только значение таргетинга, а не вкл/выкл).


### Датафлоу

Классический ESS-процессор для транспорта в БК (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения в корректировках в MySQL - `hierarchical_multipliers`, `*_multiplier_values`, `retargeting_goals`, `campaigns`... (они приходят в ESS-процессор из ESS-роутера через `LogBroker`).
- По полученным событиям достает из MySQL актуальные данные.
- Отправляет обновленные данные в реплицируемую таблицу* [markov.//home/adv/DirectMultipliers](https://yt.yandex-team.ru/markov/navigation?path=//home/adv/DirectMultipliers).

* Актуальные пути к таблицам формируется на основе поля `dynamic-yt/tables/bs-export/multipliers` в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf).

### Способы наблюдения за текущим состоянием

- [Общий дашборд ESS](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production&b=2021-03-14T09%3A41%3A19.102Z&e=2021-03-15T09%3A41%3A19.102Z)
- [Дашборд по ESS-транспорту](https://solomon.yandex-team.ru/?project=direct&dashboard=new-bs-transport)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fexport-bs-multipliers&b=1d&e=)
- [Логи событий изменения](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--export-bs-multipliers)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи экспорта](https://direct.yandex.ru/logviewer#~(logType~'bsexport_data~form~(fields~(~'log_time~'data_type~'cid~'pid~'bid~'data)~conditions~(data_type~'multiplier)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи процессора](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'multipliers.BsExportMultipliersProcessor)~limit~1000~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportMultipliersProcessor.working.production&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы

Доставка в БК изменений в корректировках (критично).


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи увидят в статистике, что при показах не учитывались новые корректировки. Это так же может привести к необходимости возврата денег.


### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

Как можно раньше.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Ломалось пока один раз, было отставание от некорректного плана запроса в mysql.


### Дополнительно: тонкости и подводные камни
