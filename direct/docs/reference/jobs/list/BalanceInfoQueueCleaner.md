## BalanceInfoQueueCleaner

### Продукт/подсистема

Интеграция с Биллингом. Нотификации в Биллинг об изменении данных клиента.


### Роль в работе продукта/подсистемы

Существует очередь ленивой отправки в Биллинг обновленных данных клиентов: [ppc.balance_info_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/balance_info_queue.html). Она обрабатывается скриптом `ppcSendBalanceInfoChanges`, отправляющим данные в метод баланса `CreateClient` (работает по схеме add-or-update). В случае успешной отправки статус записи в очереди меняется на `Send`, в случае ошибки на `Error`.

Данная джоба очищает эту очередь от уже отработанных записей.

### Датафлоу

- Удаляет из таблицы [ppc.balance_info_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/balance_info_queue.html) записи в статусе `Send` и записи в статусе `Error` старше `LIMIT_AGE_DAYS` (константа в [коде джобы](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/balance/BalanceInfoQueueCleaner.java)).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BalanceInfoQueueCleaner.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'balance.BalanceInfoQueueCleaner)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- Джоба сохраняет дату последнего полезного запуска в ppc-property `CLEAR_BALANCE_INFO_QUEUE_SHARD_{N}`, чтобы не делать работу повторно.


### Какая функциональность пострадает от отказа джобы

В случае отказа джобы в очереди баланса будут накапливаться ненужные записи.
В короткой перспективе функциональность не пострадает. Со временем возможны побочные эффекты от большого размера очереди.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи не заметят.


### Контакты разработчиков и менеджеров

Разработчики: [Паша Новоселов](https://staff.yandex-team.ru/pashkus), [Саша Дуплищев](https://staff.yandex-team.ru/ppalex).


### Желательное время исправления в случае поломки

Джоба выглядит как гигиеническая процедура. Допустимо чинить в течение недели.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
