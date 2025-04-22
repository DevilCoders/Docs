## BsExportCampaignProcessor

### Продукт/подсистема

ESS-транспорт в БК/CaeSaR.


### Роль в работе продукта/подсистемы

ESS транспорт информации о кампаниях в БК/CaeSaR. Группы и баннеры отправляются отдельными джобами.


### Датафлоу

Классический ESS-процессор для транспорта в БК (см. [ESS-контур](../../../ess/howto-code.md)).

- Отслеживает изменения в кампаниях в MySQL (они приходят в ESS-процессор из ESS-роутера через `LogBroker`).
- По полученным событиям достает из MySQL актуальные данные.
- Отправляет обновленные данные в реплицируемую таблицу* [markov.//home/adv/DirectCampaigns](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/adv/DirectCampaigns).
- И в очередь Caesar [markov.//home/adv/queues/DirectCampaignsQueue](https://yt.yandex-team.ru/markov/navigation?path=//home/adv/queues/DirectCampaignsQueue).

* Актуальные пути к таблицам формируется на основе поля `dynamic-yt/tables/bs-export/campaigns` в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf).

### Способы наблюдения за текущим состоянием

- [ESS-дашборд](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production)
- [Дашборд по ESS-транспорту](https://solomon.yandex-team.ru/?project=direct&dashboard=new-bs-transport)
- [График отставания вычитки топика](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=*&graph=auto&l.TopicPath=direct%2Fess%2Fexport-bs-campaigns&b=2021-03-21T14%3A18%3A10.000Z&e=2021-03-22T14%3A18%3A10.000Z)
- [Логи событий изменения](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--export-bs-campaigns)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи экспорта](https://direct.yandex.ru/logviewer#~(logType~'bsexport_data~form~(fields~(~'log_time~'data_type~'cid~'pid~'bid~'data)~conditions~(data_type~'campaign)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'campaign.BsExportCampaignProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportCampaignProcessor.working.production&last=1DAY&query=)


### Какая функциональность пострадает от отказа джобы

Отправка кампаний новым транспортом в БК. На текущий момент (2021-03-22) критичными являются ресурсы внутренних кампаний. При поломке джобы страдают все ресурсы кампаний.


### Как пользователи (или команда) заметят проблему и через какое время

При показах не будут отображаться или будут отображаться некорректно некоторые данные по кампании, в БК будут неверные минус фразы и пр.


### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)
БК: [Данил Григорьевых](https://staff.yandex-team.ru/danilgrig), [Искандер Ямбулатов](https://staff.yandex-team.ru/yambulatov), [Фёдор Строк](https://staff.yandex-team.ru/fdrstrok)
По ресурсам внутренней рекламы: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Женя Козобродов](https://staff.yandex-team.ru/kozobrodov)

### Желательное время исправления в случае поломки

Как можно раньше.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

- Проблемы с LogBroker.
- Работы на YT кластере Markov.
- Не работает весь ESS-контур.


### Дополнительно: тонкости и подводные камни
