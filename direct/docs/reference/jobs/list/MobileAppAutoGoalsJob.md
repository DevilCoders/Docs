## MobileAppAutoGoalsJob

### Продукт/подсистема

Реклама мобильных приложений


### Роль в работе продукта/подсистемы

Добавляет в таблицу [mobile_app_goals_external_tracker](https://direct-dev.yandex-team.ru/db/ppc/tables/mobile_app_goals_external_tracker.html) новые цели с событиям по которым приходили постбеки от трекеров


### Датафлоу

Джоба читает из YT-таблицы [DirectMobileAppStat](https://yt.yandex-team.ru/seneca-vla/navigation?offsetMode=key&path=//home/yabs/stat/DirectMobileAppStat) события сгруппированные по приложениям и добавляет в таблицу `mobile_app_goals_external_tracker` цели с событиями, которых ещё не было у приложений


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MobileAppAutoGoalsJob.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'mobilegoals.MobileAppAutoGoalsJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будут автоматически заводиться цели на основе данных постбеков


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи не увидят целей, которые добавились автоматически на основе данных постбеков


### Контакты разработчиков и менеджеров

Разработчики: [Роман Иванов](https://staff.yandex-team.ru/nbahob) <br/>
Менеджеры: [Вадим Костомаров](https://staff.yandex-team.ru/nevadimka), [Владимир Недашковский](https://staff.yandex-team.ru/texnedo)


### Желательное время исправления в случае поломки

День


### Способы регулирования работы джобы

- джоба включается PpcProperty [MOBILE_APPS_AUTO_GOALS_JOB_ENABLED](https://direct.yandex.ru/internal_tools/#set_typed_ppc_property)


### Известные причины поломок

Проблемы с YT `seneca-*`


### Дополнительно: тонкости и подводные камни
