## AggregatedStatusesMonitorJob

### Продукт/подсистема

Агрегированные статусы.


### Роль в работе продукта/подсистемы

Мониторинг расчета агрегированных статусов для нового интерфейса Директа.

Джоба считает общее количество записей агрегированных статусов объектов (кампании, баннеры, группы и т. д) с `is_obsolete=1` без учета времени, и отдельно количество записей у которых `is.obsolete=1` стоит больше 15 минут. Посчитанные данные отправляются в Соломон.


### Датафлоу

Делает [yql-запрос](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/aggregatedstatuses/is_obsolete_totals_report.yql) в выгрузку базы директа в YT на кластерах Hahn, Arnold, результат отправляет в Solomon.


### Способы наблюдения за текущим состоянием

- [Графики в Solomon](https://nda.ya.ru/t/p8VdbR0B3qx9a7)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.AggregatedStatusesMonitorJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'monitoring.AggregatedStatusesMonitorJob~service~'direct.jobs)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будет новых данных по агрегированным статусам в Solomon.


### Как пользователи (или команда) заметят проблему и через какое время

Команда может заметить сломанные графики в Solomon.


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Гукасьян](https://staff.yandex-team.ru/gukserg)


### Желательное время исправления в случае поломки

Неделя.


### Способы регулирования работы джобы

-


### Известные причины поломок

- Проблемы с доступностью кластеров Hahn, Arnold.
- Изменения в синтаксисе YQL-запросов.


### Дополнительно: тонкости и подводные камни
