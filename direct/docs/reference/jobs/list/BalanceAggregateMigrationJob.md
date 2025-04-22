## BalanceAggregateMigrationJob

**TODO: уточнить и дополнить**

### Продукт/подсистема

Интеграция с Биллингом.


### Роль в работе продукта/подсистемы

Переводит кампании-кошельки на новую схему зачислений.


### Датафлоу

- Берет задачи на перевод кампании-кошелька (`campaigns.type = 'wallet'`) на новую схему зачислений из очереди [ppc.dbqueue_jobs](https://direct-dev.yandex-team.ru/db/ppc/tables/dbqueue_jobs.html).
- Переводит (делает модификации в MySQL, добавляет кампании в очередь на переотправку в БК (`bsexport_specials`)).

На данный момент задания в очередь добавляются при создании биллинговых агрегатов из создания кампаний в джаве (`BillingAggregateService.createBillingAggregates`). Что видится несколько странной схемой перевода кошельков на новую схему зачислений. Сейчас примерно 40% кошельков переведено, а джобу запустили в ноябре 2018.

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BalanceAggregateMigrationJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'balanceaggrmigration.BalanceAggregateMigrationJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы




### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko)


### Желательное время исправления в случае поломки

?


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни
