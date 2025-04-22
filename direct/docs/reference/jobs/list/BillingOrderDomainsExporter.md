## BillingOrderDomainsExporter

### Продукт/подсистема

Агентские комиссии.


### Роль в работе продукта/подсистемы

Запускает YQL запрос который делает расчет комиссий для агентств и сохраняет результат в виде таблицы в YT (потребитель - Биллинг).


### Датафлоу

[Код YQL-скрипта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/export/BillingOrderDomains.sql).
Скрипт делает вычисления в YT и выгружает результаты в две таблицы: [//home/direct/export/balance/BillingOrderDomains](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/balance/BillingOrderDomains) и [//home/direct/export/balance/BillingOrderDomainsSplittedStat](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/balance/BillingOrderDomainsSplittedStat).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BillingOrderDomainsExporter.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'export.BillingOrderDomainsExporter)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Комиссии перестанут рассчитываться для агентств.


### Как пользователи (или команда) заметят проблему и через какое время

Данные от этой джобы используются раз в месяц в Биллинге.


### Контакты разработчиков и менеджеров

Разработчики: [Алексей Кашицын](https://staff.yandex-team.ru/aliho)


### Желательное время исправления в случае поломки

День.


### Способы регулирования работы джобы

-


### Известные причины поломок

-


### Дополнительно: тонкости и подводные камни

Есть тикет по выпиливанию всего этого в пользу DWH: https://st.yandex-team.ru/DIRECT-130070
