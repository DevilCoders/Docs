## BsExportBannerResourcesProcessor

### Продукт/подсистема

ESS-транспорт в БК/CaeSaR.


### Роль в работе продукта/подсистемы

Асинхронный ESS транспорт ресурсов баннеров (ассетов, кусочков) в БК/CaeSaR. Получает события, что в БД изменилась информация о баннерах и экспортирует информацию об этих изменениях в БК. Асинхронный в том смысле, что обязательная часть баннера и его ресурсы отправляются независимо во времени.


### Датафлоу

Классический ESS-процессор для транспорта в БК (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения в ресурсах баннеров в MySQL (они приходят в ESS-процессор из ESS-роутера через `LogBroker`).
- По полученным событиям достает из MySQL актуальные данные.
- Отправляет обновленные данные в реплицируемую таблицу [markov.//home/adv/DirectBannerResources](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/adv/DirectBannerResources).
- И в очередь Caesar [markov.//home/adv/queues/DirectBannerResourcesQueue](https://yt.yandex-team.ru/markov/navigation?path=//home/adv/queues/DirectBannerResourcesQueue).

* Актуальные пути к таблицам формируется на основе поля `dynamic-yt/tables/bs-export/banner-resources` в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf).

### Способы наблюдения за текущим состоянием

- [ESS-дашборд](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production)
- [Дашборд по ESS-транспорту](https://solomon.yandex-team.ru/?project=direct&dashboard=new-bs-transport)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fexport-bs-banner-resources&b=2021-03-21T14%3A18%3A10.394Z&e=2021-03-22T14%3A18%3A10.394Z)
- [Логи событий изменения](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--export-bs-banner-resources)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи экспорта](https://direct.yandex.ru/logviewer#~(logType~'bsexport_data~form~(fields~(~'log_time~'data_type~'cid~'pid~'bid~'data)~conditions~(data_type~'banner_resources)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'resources.BsExportBannerResourcesProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportBannerResourcesProcessor.working.production&query=&last=1DAY)


### Какая функциональность пострадает от отказа джобы

Отправка ресурсов баннеров новым транспортом в БК. На текущий момент (2021-03-22) критичными ресурсами являются кнопка и логотип. При поломке джобы страдают все ресурсы баннера.


### Как пользователи (или команда) заметят проблему и через какое время

- До показов не будут доезжать новые ресурсы (баннеры будут крутиться без них).
- До показов не доедут новые версии уже отправленных ресурсов (баннеры будут продолжать крутиться с устаревшими версиями ресурсов).


### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Марина Спиридонова](https://staff.yandex-team.ru/mspirit)
БК: [Данил Григорьевых](https://staff.yandex-team.ru/danilgrig), [Искандер Ямбулатов](https://staff.yandex-team.ru/yambulatov), [Фёдор Строк](https://staff.yandex-team.ru/fdrstrok)


### Желательное время исправления в случае поломки

Как можно раньше.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

- Проблемы с LogBroker.
- Работы на YT кластере Markov.
- Не работает весь ESS-контур.


### Дополнительно: тонкости и подводные камни
