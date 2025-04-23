## ModerationFlagsEventsProcessor

### Продукт/подсистема

Транспорт в Модерацию


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию события изменения пользователем флагов баннеров.


### Датафлоу

Процессор обрабатывает события изменения флагов и отправляет уведомления в Модерацию.

- Отслеживает добавление/изменение записей в таблице [banner_user_flags_updates](https://direct-dev.yandex-team.ru/db/ppc/tables/banner_user_flags_updates.html).
- Отправляет событие об изменении флагов в Модерацию через LogBroker.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ModerationFlagsEventsProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'flags.ModerationFlagsEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию события изменения флагов, Модерация будет модерировать баннер с устаревшей информацией о пользовательских флагах.


### Как пользователи (или команда) заметят проблему и через какое время

Команда Модерации заметит, что не приходят события обновления флагов.


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
