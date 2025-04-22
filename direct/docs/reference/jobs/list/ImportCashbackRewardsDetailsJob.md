## ImportCashbackRewardsDetailsJob

### Продукт/подсистема

Программа лояльности пользователей — начисление пользователям кешбэков за использование определённой функциональности в Директе.


### Роль в работе продукта/подсистемы

Раз в месяц Биллинг вычисляет суммы кешбэков, исходя из включенных пользователю программ и того, как он пользовался различной функциональностью директа. Эта детализация для каждого пользователя складывается в таблицу в YT. Данная джоба  забирает эти данные из YT и перекладывает их в MySQL Директа, чтобы в последствии можно было отобразить клиенту в интерфейсе историю начисления кешбэков.


### Датафлоу

- Читает данные из таблиц в YT в директории: [home/balance/prod/yb-ar/cashback/export](https://yt.yandex-team.ru/hahn/navigation?path=//home/balance/prod/yb-ar/cashback/export).
- Для каждого кластера (пока только Hahn) ищет в директории таблицы с названием вида "yyyyMM", начиная с даты, заданной ppc-property `last_imported_cashback_month`. Если таблица найдена на одном кластере, на остальных поиск той же таблицы осуществлён не будет.
- Найденные таблицы импортируются в MySQL в таблицы [ppc.clients_cashback_details](https://direct-dev.yandex-team.ru/db/ppc/tables/clients_cashback_details.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ImportCashbackRewardsDetailsJob.working.production&query=&last=1DAY).
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'cashback.ImportCashbackRewardsDetailsJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Детализация начисленных кешбэков для клиентов в интерфейсе — средне-критично. После восстановления клиенты получат нормальную картину в визарде.


### Как пользователи (или команда) заметят проблему и через какое время?

Табличка с данными за предыдущий месяц не появится, пока джоба не заведется.


### Контакты разработчиков и менеджеров

Директ: [Женя Козобродов](https://staff.yandex-team.ru/kozobrodov), [Сережа Ковач](https://staff.yandex-team.ru/buhter) <br/>
Биллинг: [Игорь Галков](https://staff.yandex-team.ru/antropod) <br/>
Менеджеры: [Сережа Ковач](https://staff.yandex-team.ru/buhter), [Паша Рябов](https://staff.yandex-team.ru/pavryabov), [Михаил Иволгин](https://staff.yandex-team.ru/mivolgin) <br/>


### Желательное время исправления в случае поломки
Зависит от времени появления новой таблицы в YT. Чем ближе поломка к появлению новой таблицы — тем более срочно надо чинить.


### Способы регулирования работы джобы

- ppc-property `import_cashback_rewards_details_enabled` — позволяет временно выключить Job. Если не задано, то Job по умолчанию выключен.

- ppc-property `last_imported_cashback_month` — содержит дату последней импортированной YT-таблицы. Если не задано, по умолчанию берётся август 2020.

### Известные причины поломок



### Дополнительно: тонкости и подводные камни
