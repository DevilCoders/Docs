### Продукт/подсистема

{% include notitle [subsystem](ReplicateToYdbJob.md#subsystem) %}


### Роль в работе продукта/подсистемы
Инфрастуктура для мониторинга за очередью.
Непосредственно в отправке данных не участвует.

Считает агрегированные данные о состоянии очереди и отправляет их в Solomon.

### Датафлоу
- джоба полагается на работу [ReplicateToYdbJob](ReplicateToYdbJob.md), которая реплицирует данные bs_export_queue из всех шардов MySQL в одну [YDB-табличку](https://ydb.yandex-team.ru/db/ydb-ru/direct/production/maintenance-helpers/browser/bs_export_queue)
- запускает поверх этой таблички YQL-запрос, считающий статистику в разных разрезах
- читает результат YQL, отправляет (через pull—механизм) метрики в [Solomon](https://solomon.yandex-team.ru/?project=direct&service=bs-export-queue&cluster=app_java-jobs)



### Способы наблюдения за текущим состоянием
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.Monitor.working.production)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'bsexportqueue.Monitor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)



### Какая функциональность пострадает от отказа джобы
Алерты и графики про состояние очереди.


### Как пользователи (или команда) заметят проблему и через какое время
Пользователи проблему заметить не могут — прямого влияния у джобы нет.

Разработчики могут:
- увидеть, что нет графиков на [дашборде](https://solomon.yandex-team.ru/?project=direct&dashboard=bs-export-perl&b=6h)
- получить срабатывания алертов с "нет данных" или ошибкой



### Контакты разработчиков и менеджеров

{% include notitle [contacts](ReplicateToYdbJob.md#contacts) %}


### Желательное время исправления в случае поломки

{% include notitle [time to fix](ReplicateToYdbJob.md#time-to-fix) %}


### Способы регулирования работы джобы

Отсутствуют


### Известные причины поломок
Если очередь в MySQL базе сильно вырастет, объем данных в YDB тоже увеличится, запросы начнут тормозить и могут перестать укладываться в таймаут.

Может что-то поломаться при выполнении YQL—запроса: попробовать понять по ошибке, что именно, либо воспроизвести запрос самому через YQL.
