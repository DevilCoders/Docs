## BsExportBiddableShowConditionsProcessor

### Продукт/подсистема

ESS-транспорт в БК/CaeSaR.


### Роль в работе продукта/подсистемы

ESS транспорт в БК/CaeSaR информации об условиях показа со ставкой (или приоритетом в случае автоматической стратегии) в БК/CaeSaR.


### Датафлоу

Классический ESS-процессор для транспорта в БК (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения в условиях показа со ставкой в MySQL (они приходят в ESS-процессор из ESS-роутера через `LogBroker`). На данный момент (27.03.2021) это следующие сущности:
  - ключевые фразы - [bids](https://direct-dev.yandex-team.ru/db/ppc/tables/bids.html);
  - автотаргетинги (aka "безфразные таргетинги") - [bids_base](https://direct-dev.yandex-team.ru/db/ppc/tables/bids_base.html);
  - условия подбора аудитории и ретаргетинги - [bids_retargeting](https://direct-dev.yandex-team.ru/db/ppc/tables/bids_retargeting.html);
  - условия нацеливания в кампаниях типа "Динамические объявления" - [bids_dynamic](https://direct-dev.yandex-team.ru/db/ppc/tables/bids_dynamic.html);
  - фильтры в кампаниях типа "Смарт-баннеры" - [bids_performance](https://direct-dev.yandex-team.ru/db/ppc/tables/bids_performance.html);
- По полученным событиям достает из MySQL актуальные данные.
- Отправляет обновленные данные в реплицируемую таблицу* [markov.//home/adv/DirectBiddableShowConditions](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/adv/DirectBiddableShowConditions).
- И в очередь Caesar* [markov.//home/adv/queues/DirectBiddableShowConditionsQueue](https://yt.yandex-team.ru/markov/navigation?path=//home/adv/queues/DirectBiddableShowConditionsQueue).

* Актуальные пути к таблицам формируется на основе поля `dynamic-yt/tables/bs-export/biddable-show-conditions` в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf).


### Способы наблюдения за текущим состоянием

- [ESS-дашборд](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production)
- [Дашборд по ESS-транспорту](https://solomon.yandex-team.ru/?project=direct&dashboard=new-bs-transport)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fexport-bs-biddable-show-conditions&b=2021-03-21T14%3A18%3A10.000Z&e=2021-03-22T14%3A18%3A10.000Z)
- [Логи событий изменения](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--export-bs-biddable-show-conditions)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи экспорта](https://direct.yandex.ru/logviewer#~(logType~'bsexport_data~form~(fields~(~'log_time~'data_type~'cid~'pid~'bid~'data)~conditions~(data_type~'biddable_show_conditions)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'bids.BsExportBiddableShowConditionsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportBiddableShowConditionsProcessor.working.production&last=1DAY&query=)


### Какая функциональность пострадает от отказа джобы

Отправка условий показа новым транспортом в БК. Баннеры либо не будут крутиться, либо будут крутиться с устаревшим условием показа и ставкой - это критично.


### Как пользователи (или команда) заметят проблему и через какое время

- Пользователи могут увидеть по статусу в интерфейсе, что баннеры не крутятся, если условие новое и из-за поломки не доехало в БК.
- Пользователи могут увидеть по статистике, что баннеры откручивались по устаревшей версии условия показа и/или ставке.


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

Максимально оперативно.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

- Проблемы с LogBroker.
- Работы на YT кластере Markov.
- Не работает весь ESS-контур.


### Дополнительно: тонкости и подводные камни
