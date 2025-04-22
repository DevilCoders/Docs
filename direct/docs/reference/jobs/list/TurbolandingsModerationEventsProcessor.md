## TurbolandingsModerationEventsProcessor

### Продукт/подсистема

Модерация ресурса баннера "Турбостраница".


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию ресурс баннера.


### Датафлоу

Классический модерационный ESS процессор.

- Отслеживает события в таблице [ppc.banner_turbolandings](https://direct-dev.yandex-team.ru/db/ppc/tables/banner_turbolandings.html).
- Отправляет ресурс в Модерацию через LogBroker.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.TurbolandingsModerationEventsProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'turbolandings.TurbolandingsModerationEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию ресурсы баннера типа "Турбостраница".


### Как пользователи (или команда) заметят проблему и через какое время

По статусу баннера увидят, что "Турбостраница" баннера долго находится в Модерации.


### Контакты разработчиков и менеджеров

Разработчики: [Денис Говорков](https://staff.yandex-team.ru/oxid)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
