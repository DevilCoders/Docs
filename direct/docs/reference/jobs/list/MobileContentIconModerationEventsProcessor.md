## MobileContentIconModerationEventsProcessor

### Продукт/подсистема

Модерация иконок мобильных приложений.


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию информацию об иконке мобильного приложения.


### Датафлоу

Классический модерационный ESS-процессор.

- [ESS-правило](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/rules/moderation/mobilecontenticon/MobileContentIconModerationRule.java) отслеживает события в таблице [mobile_content](https://direct-dev.yandex-team.ru/db/ppc/tables/mobile_content.html), поле statusIconModerate.
- Логические события пишутся в топик [ess--mobile-content-icon-moderation](https://logbroker.yandex-team.ru/lbkx/accounts/direct/ess/mobile-content-icon-moderation?page=statistics&type=topic)
- [ESS-процессор](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/moderation/mobilecontenticon/MobileContentIconModerationEventsProcessor.java) отправляет запрос в Модерацию через [LogBroker-топик](https://logbroker.yandex-team.ru/lbkx/accounts/modadvert/prod/direct/mobile_icon?page=statistics&type=topic).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MobileContentIconModerationEventsProcessor.working.production&query=&last=1DAY)
- [Логические события](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--mobile-content-icon-moderation)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'mobilecontenticon.MobileContentIconModerationEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))
- [Отправленные запросы в Модерацию](https://direct.yandex.ru/logviewer#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(data~'*25mobile_icon*25~action~'request)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию иконки мобильных приложений.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи увидят, что их мобильные приложения не отмодерированы.


### Контакты разработчиков и менеджеров

Разработчики: [Алексей Володских](https://staff.yandex-team.ru/volodskikh)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
