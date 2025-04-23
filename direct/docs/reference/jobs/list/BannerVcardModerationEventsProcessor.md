## BannerVcardModerationEventsProcessor

### Продукт/подсистема

Модерация ресурса баннера "Визитка".


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию ресурс баннера.


### Датафлоу

Классический модерационный ESS-процессор.

- [ESS-правило](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/rules/moderation/asset/BannerVcardModerationRule.java) отслеживает события в таблице [ppc.banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html), поле phoneflag.
- Логические события пишутся в топик [ess--asset-moderation-vcard](https://logbroker.yandex-team.ru/lbkx/accounts/direct/ess/asset-moderation-vcard?page=statistics&type=topic)
- [ESS-процессор](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/moderation/asset/BannerVcardModerationEventsProcessor.java) отправляет запрос в Модерацию через [LogBroker-топик](https://logbroker.yandex-team.ru/lbkx/accounts/modadvert/prod/direct/asset_vcard?page=statistics&type=topic).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BannerVcardModerationEventsProcessor.working.production&query=&last=1DAY)
- [Логические события](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--asset-moderation-vcard)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'asset.BannerVcardModerationEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))
- [Отправленные запросы в Модерацию](https://direct.yandex.ru/logviewer#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(data~'*25asset_vcard*25~action~'request)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию "Визитки".


### Как пользователи (или команда) заметят проблему и через какое время

По статусу баннера увидят, что "Визитки" баннера долго находится в Модерации.


### Контакты разработчиков и менеджеров

Разработчики: [Алексей Володских](https://staff.yandex-team.ru/volodskikh)


### Желательное время исправления в случае поломки

Как можно скорее.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
