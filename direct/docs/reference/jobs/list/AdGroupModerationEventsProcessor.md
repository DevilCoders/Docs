## AdGroupModerationEventsProcessor

### Продукт/подсистема

Модерация групп.


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию группы: отправка носит уведомительный характер, не ждем вердиктов на группы, группы и фразы автопринимаются после отправки.


### Датафлоу

Классический модерационный ESS процессор.

- [ESS-правило](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/rules/moderation/adgroup/AdGroupModerationRule.java) отслеживает события в таблице [phrases](https://direct-dev.yandex-team.ru/db/ppc/tables/phrases.html).
- Логические события пишутся в топик [ess--adgroup-moderation](https://logbroker.yandex-team.ru/lbkx/accounts/direct/ess/adgroup-moderation?page=statistics&type=topic)
- [ESS-процессор](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/moderation/adgroup/AdGroupModerationEventsProcessor.java) отправляет запрос в Модерацию через [LogBroker-топик](https://logbroker.yandex-team.ru/lbkx/accounts/modadvert/prod/direct/adgroup?page=statistics&type=topic).
- После отправки в Модерацию процессор переводит группы и связанные с ними фразы в `statusModerate=Yes`.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.AdGroupModerationEventsProcessor.working.production&query=&last=1DAY)
- [Логические события](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--adgroup-moderation)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'adgroup.AdGroupModerationEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Отправленные запросы в Модерацию](https://direct.yandex.ru/logviewer#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(data~'*25adgroup*25~action~'request)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию группы и не будет происходить автопринятие групп.


### Как пользователи (или команда) заметят проблему и через какое время

По статусу группы пользователи увидят, что он долго находится в Модерации.


### Контакты разработчиков и менеджеров

Разработчики: [Роман Шевченко](https://staff.yandex-team.ru/stasis93), [Алексей Володских](https://staff.yandex-team.ru/volodskikh)


### Желательное время исправления в случае поломки

Как можно скорее.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
