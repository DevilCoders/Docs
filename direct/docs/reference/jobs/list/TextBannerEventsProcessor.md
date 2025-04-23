## TextBannerEventsProcessor

### Продукт/подсистема

Модерация текстовых баннеров.
Типы баннеров: `text`.


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию баннеры указанных типов.


### Датафлоу

Классический модерационный ESS процессор.

- [ESS-правило](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/rules/moderation/banner/TextBannerModerationRule.java) отслеживает события в таблице [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html) для баннеров указанных типов.
- Логические события пишутся в топик [ess--banner-moderation-text](https://logbroker.yandex-team.ru/lbkx/accounts/direct/ess/banner-moderation-text?page=statistics&type=topic)
- [ESS-процессор](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/moderation/banner/TextBannerEventsProcessor.java) отправляет запрос в Модерацию через [LogBroker-топик](https://logbroker.yandex-team.ru/lbkx/accounts/modadvert/prod/direct/text_banner?page=statistics&type=topic).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.TextBannerEventsProcessor.working.production&query=&last=1DAY)
- [Логические события](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--banner-moderation-text)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'banner.TextBannerEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Отправленные запросы в Модерацию](https://direct.yandex.ru/logviewer#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(data~'*25text_sm*25~action~'request)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию баннеры.


### Как пользователи (или команда) заметят проблему и через какое время

По статусу баннера увидят, что он долго находится в Модерации.


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
