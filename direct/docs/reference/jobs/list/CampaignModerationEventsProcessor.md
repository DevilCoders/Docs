## CampaignModerationEventsProcessor

### Продукт/подсистема

Модерация кампаний.


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию кампании: отправка носит уведомительный характер, не ждем вердиктов на кампании, статус кампании пересчитывает отдельная джоба `CampaignStatusEventsProcessor`.
Также отправляет события копирования кампаний: модерация хочет знать, что кампания была скопирована с какой-то другой.


### Датафлоу

Классический модерационный ESS процессор.

- [ESS-правило](https://a.yandex-team.ru/svn/trunk/arcadia/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/rules/moderation/campaign/CampaignModerationRule.java) отслеживает события в таблице [phrases](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns.html).
- Логические события пишутся в топик [ess--moderation-special-campaign-copy](https://logbroker.yandex-team.ru/lbkx/accounts/direct/ess/moderation-special-campaign-copy?page=statistics&type=topic). Название не совсем соответствует процессору, но изначально процессор отправлял только события копирования кампаний.
- [ESS-процессор](https://a.yandex-team.ru/svn/trunk/arcadia/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/moderation/campaign/CampaignModerationEventsProcessor.java) отправляет запрос в Модерацию через [LogBroker-топик для событий модерации](https://logbroker.yandex-team.ru/lbkx/accounts/modadvert/prod/direct/campaign_sm?page=statistics&type=topic) и [LogBroker-топик для событий копирования](https://logbroker.yandex-team.ru/lbkx/accounts/modadvert/prod/direct/add-copycamp-objects?page=statistics&type=topic).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CampaignModerationEventsProcessor.working.production&query=&last=1DAY)
- [Логические события](https://direct.yandex.ru/logviewer#~(logType~'ess_logic_objects~form~(fields~(~'binlog_time~'topic~'source~'logic_object~'reqid)~conditions~(topic~'*25ess--moderation-special-campaign-copy)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))
- [Логи процессора](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'campaign.CampaignModerationEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Отправленные запросы в Модерацию](https://direct.yandex.ru/logviewer#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(data~'*25campaign_sm*25~action~'request)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию кампании.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи проблему не заметят, незначительно деградирует качество модерации новых баннеров.


### Контакты разработчиков и менеджеров

Разработчики: [Алексей Володских](https://staff.yandex-team.ru/volodskikh)
Команда модерации: [Владислав Невструев](https://staff.yandex-team.ru/nevstrui), [Виталий Суворов](https://staff.yandex-team.ru/vsuvorov)


### Желательное время исправления в случае поломки

В течение дня.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
