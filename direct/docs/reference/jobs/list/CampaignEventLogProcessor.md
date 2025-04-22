## CampaignEventLogProcessor

### Продукт/подсистема

Бюджет, стратегии.


### Роль в работе продукта/подсистемы

ESS-процессор обрабатывает изменения бюджета кампаний и делает запись о произошедшем событии в [ppc.eventlog](https://direct-dev.yandex-team.ru/db/ppc/tables/eventlog.html). Эта запись влияет на показ плашки рекомендаций и теоретически еще на что угодно, так как табличка достаточно общая и содержит различные важные события с кампаниями, группами, баннерами.

Изначально делалось для плашки рекомендаций недельного бюджета в тикете [DIRECT-104972](https://st.yandex-team.ru/DIRECT-104972).


### Датафлоу

- ESS-процессор ловит нужные изменения в MySQL.
- Записывает данные в табличку [ppc.eventlog](https://direct-dev.yandex-team.ru/db/ppc/tables/eventlog.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CampaignEventLogProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'campeventlog.CampaignEventLogProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Общая функциональность по пбликации событий в [ppc.eventlog](https://direct-dev.yandex-team.ru/db/ppc/tables/eventlog.html).


### Как пользователи (или команда) заметят проблему и через какое время

Примеры:
- Плашка рекомендаций не будет получать актуальные данные ([DIRECT-107535](https://st.yandex-team.ru/DIRECT-107535)).


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Димитров](https://staff.yandex-team.ru/dimitrovsd), [Сергей Ирин](https://staff.yandex-team.ru/snirinn)


### Желательное время исправления в случае поломки

Как можно раньше.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
