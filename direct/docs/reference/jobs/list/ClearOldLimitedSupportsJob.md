## ClearOldLimitedSupportsJob

### Продукт/подсистема

Система ролей.


### Роль в работе продукта/подсистемы

Роль `limited_support` - ограниченный саппорт (по правам похож на менеджера). Роли заводятся в idm и оттуда вызывается наша ручка. Там можно удалить роль и вызовется ручка `remove_role` (попытаемся поменять `limited_support` на `empty`). Но если есть привязанные клиенты, то не отбираем сразу роль, а блокируем - `users.status_block`. Спустя какое-то время клиенты отвяжутся.

Данная джоба находит заблокированных пользователей с ролью `limited_support` без привязанных клиентов и отбирает роль.


### Датафлоу

- Находим всех пользователей с `role=limited_support` и `statusBlocked = Yes`
- Для тех, у которых больше нет связанных ролей `support_for_client` (записей в [ppc.clients_relations](https://direct-dev.yandex-team.ru/db/ppc/tables/clients_relations.html) `type = support_for_client`), меняем роль: `clients.role limited_support -> 'empty'` и разблокируем: `users.statusBlocked Yes -> No`.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ClearOldLimitedSupportsJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'idm.ClearOldLimitedSupportsJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Неделя.


### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [Анастасия Лобанова](https://staff.yandex-team.ru/a-lobanova), [Максим Логунов](https://staff.yandex-team.ru/maxlog)


### Желательное время исправления в случае поломки




### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
