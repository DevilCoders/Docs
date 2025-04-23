## ResendFrontpageCampaignsBeforeStartDatetoBSJob

### Продукт/подсистема

Компании на главной странице Яндекса.


### Роль в работе продукта/подсистемы

Переотправляет в бк компании, у которых дата старта завтрашний день. Это нужно чтобы избежать геноцида компаний.


### Датафлоу

Шардированная джоба, взаимодействует с MySQL.

Вытягивает компании на морде с датой старта - следующий день.
Ставит им statusBsSynced = No - это переотправляет их в бк.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ResendFrontpageCampaignsBeforeStartDatetoBSJob.working.production&project=direct.prod&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'intermediate.ResendFrontpageCampaignsBeforeStartDatetoBSJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Некоторые компании на главной страницы Яндекса будут умирать из-за геноцида и их придется переотправлять вручную.


### Как пользователи (или команда) заметят проблему и через какое время

Компании на главной страницы Яндекса иногда будут умирать из-за геноцида.


### Контакты разработчиков и менеджеров

Разработчики: [Александр Кулаков](https://staff.yandex-team.ru/alex-kulakov)


### Желательное время исправления в случае поломки

Неделя.


### Способы регулирования работы джобы



### Известные причины поломок




### Дополнительно: тонкости и подводные камни
