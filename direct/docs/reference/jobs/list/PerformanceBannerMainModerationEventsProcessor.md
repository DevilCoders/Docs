## PerformanceBannerMainModerationEventsProcessor

### Продукт/подсистема

Автопринятие новых родительских performance-баннеров

### Роль в работе продукта/подсистемы

Автопринимает новые родительские performance-баннеры. В будущем ещё и будет отправлять в Модерацию информацию по этим баннерам.

### Датафлоу

Модерационный ESS-процессор, только не отправляет в Модерацию, а автоматически принимает баннеры

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.PerformanceBannerMainModerationEventsProcessor.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'banner.PerformanceBannerMainModerationEventsProcessor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы

Не будут автоприниматься (и отправляться в БК) баннеры (критично)

### Как пользователи (или команда) заметят проблему и через какое время

Пользователи рано или поздно заметят, что кампания так и не начала показываться, могут начать жаловаться

### Контакты разработчиков и менеджеров

Разработчики: [Игорь Костромин](https://staff.yandex-team.ru/elwood)

### Желательное время исправления в случае поломки

Как можно раньше

### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)

### Известные причины поломок

### Дополнительно: тонкости и подводные камни
