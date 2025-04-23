## ModerationResponsesTimeMonitoringJob

### Продукт/подсистема

Модерация в целом.


### Роль в работе продукта/подсистемы

Джоба, которая строит график количества объектов, на которые не пришло ответа из модерации за определенное время.


### Датафлоу

- По логу `ess_moderation` за неделю находит объекты, на которые не был получен вердикт за заданное время (сейчас 8 часов).
- Логгирует некоторое количество таких объектов в лог `messages`.
- Пушит количество объектов в соломон.


### Способы наблюдения за текущим состоянием

- [График, который строит джоба](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs-push&service=push-monitoring&l.jobs=moderation_responses_monitoring&l.env=production&graph=auto&l.host=CLUSTER&downsamplingFill=previous&b=7d&e=)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ModerationResponsesTimeMonitoringJob.working.production&last=1DAY&query=)
- [Логи джобы](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'moderation.ModerationResponsesTimeMonitoringJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$). Там же можно посмотреть примеры объектов, вердикты на которые ещё ждем.


### Какая функциональность пострадает от отказа джобы

Перестанет строиться график количества объектов, на которые ждем вердиктов.


### Как пользователи (или команда) заметят проблему и через какое время

Никак, только мониторинг.


### Контакты разработчиков и менеджеров

Разработчики: [Алексей Володских](https://staff.yandex-team.ru/volodskikh), [Игорь Костромин](https://staff.yandex-team.ru/elwood)


### Желательное время исправления в случае поломки

В течение нескольких дней.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
