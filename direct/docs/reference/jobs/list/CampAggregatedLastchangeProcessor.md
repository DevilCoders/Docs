## CampAggregatedLastchangeProcessor

### Продукт/подсистема

Все типы кампаний. Обновление поля `LastChange` таблицы [campaigns](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns.html) на основе изменений вложенных объектов. Может использоваться максимально широко.


### Роль в работе продукта/подсистемы

Cледит за изменениями таблиц `banners`, `banner_images`, `phrases` и обновляет `campaigns.LastChange`.

Примеры использования:
- В API в методе [checkCampaigns](https://yandex.ru/dev/direct/doc/ref-v5/changes/checkCampaigns.html).

### Датафлоу

ESS-процессор.

- Следит за добавлением объектов в таблицы `banners`, `phrases`, `banner_images`, а так же за измененями полей `last_change` в этих таблицах.
- Для этих объектов обновляет поле `LastChange` соответствующей кампании.
- Обновляет ppc-property `camp_aggregated_lastchange_high_boundary_shard_<n>` - время самого последнего обновления кампании в шарде.


### Способы наблюдения за текущим состоянием

- [График](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.env=production&l.sensor=max_last_change&graph=auto&l.shard=*&l.ess_processor=camp_aggregated_last_change&stack=false&b=2021-03-12T01%3A47%3A58.232Z&e=2021-03-12T13%3A47%3A58.232Z) максимального `last_change` должен расти.
- Ppc-property 'camp_aggregated_lastchange_high_boundary_shard_<n>' должна содержать максимальный last_change для шарда.
- [Общий дашборд ESS](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production&b=2021-03-14T09%3A41%3A19.102Z&e=2021-03-15T09%3A41%3A19.102Z)
- [Отставание обработки событий по шардам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=binlog_delay&l.shard=*&graph=auto&l.ess_processor=camp_aggregated_last_change&stack=false&b=2021-03-14T09%3A44%3A07.000Z&e=2021-03-15T09%3A44%3A07.000Z)
- [Количество обработанных объектов по шардам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=logic_objects_count&l.shard=*&graph=auto&l.ess_processor=camp_aggregated_last_change&transform=differentiate&b=2021-03-14T09%3A44%3A39.000Z&e=2021-03-15T09%3A44%3A39.000Z)
- [График отставания вычитки топика ESS-роутером](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=dc-unknown&graph=auto&l.TopicPath=direct%2Fess%2Fcamp-aggregate-last-change&b=2021-03-08T09%3A48%3A49.000Z&e=2021-03-15T09%3A48%3A49.000Z)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CampAggregatedLastchangeProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'campaignlastchange.CampAggregatedLastchangeProcessor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

- Сломается обновление поля `campaigns.LastChange` с потенциально широким спектром последствий.
- В API метод `Changes.checkCampaigns` возвращает временную метку, с которой клиенты должны запрашивать последующие изменения. Значение этой временной метки берется из ppc-property `camp_aggregated_lastchange_high_boundary_shard_<n>`. Если значение не будет меняться, пользователи будут запрашивать данные по давно измененным кампаниям и тратить лишние баллы. Так же вероятно может пострадать бизнес-логика на клиентах.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи апи могут заметить некорректную работу `Changes.checkCampains`. Пример: [DIRECT-100600](https://st.yandex-team.ru/DIRECT-100600).


### Контакты разработчиков и менеджеров

Разработчики: [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

Максимально быстро.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Общие проблемы с LogBroker, ESS.


### Дополнительно: тонкости и подводные камни
