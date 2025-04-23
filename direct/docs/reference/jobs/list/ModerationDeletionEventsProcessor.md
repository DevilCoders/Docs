## ModerationDeletionEventsProcessor

### Продукт/подсистема

Транспорт в Модерацию


### Роль в работе продукта/подсистемы

ESS-процессор отправляет в Модерацию события удаления различных объектов: баннера, ассеты, группы.


### Датафлоу

Процессор обрабатывает события удаления объектов и отправляет уведомления в Модерацию.

- Отслеживает удаления в таблицах баннеров, ассетов и групп.
- Отправляет событие об удалении в Модерацию через LogBroker.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ModerationDeletionEventsProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'deletion.ModerationDeletionEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false)))


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию события удаления, в Модерации не будет прочищаться база объектов.


### Как пользователи (или команда) заметят проблему и через какое время

Команда Модерации заметит, что не приходят уведомления о Модрации и не очищается база объектов.


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
