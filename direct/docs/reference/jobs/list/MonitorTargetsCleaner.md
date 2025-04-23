## MonitorTargetsCleaner

### Продукт/подсистема

Транспорт в БК.


### Роль в работе продукта/подсистемы

Очистка таблицы [monitor.monitor_values_sec](https://direct-dev.yandex-team.ru/db/monitor/tables/monitor_values_sec.html) от старых значений


### Датафлоу

Ищет в таблице [monitor.monitor_values_sec](https://direct-dev.yandex-team.ru/db/monitor/tables/monitor_values_sec.html) в базе monitor значенения старше 30 дней и удаляет их.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MonitorTargetsCleaner.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(from~'20210329T000000~to~'20210329T235959~fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'monitortargets.MonitorTargetsCleaner~service~'direct.jobs)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Таблица используется в транспорте БК `BSExportMaster.pm` и скрипте `ppcRetargetingCheckGoalsMonitor.pl` для джоинов. Возможно замедление работы этих процессов, если таблица станет слишком большой.


### Как пользователи (или команда) заметят проблему и через какое время

-


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Гукасьян](https://staff.yandex-team.ru/gukserg)


### Желательное время исправления в случае поломки

Неделя.


### Способы регулирования работы джобы

-


### Известные причины поломок

-


### Дополнительно: тонкости и подводные камни

-
