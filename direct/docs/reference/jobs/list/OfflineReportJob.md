## OfflineReportJob

### Продукт/подсистема

Отчёты для агентств.


### Роль в работе продукта/подсистемы

Показывает для агенств параметры, от которых зависит их премия. Отчёт интересен агенствам в начале квартала.


### Датафлоу

- Джоба берёт из очереди в таблице [ppc.offline_reports](https://direct-dev.yandex-team.ru/db/ppc/tables/offline_reports.html) задачу на построение отчёта.
- Строит отчёт по данным Биллинга в `Hahn`.
- Загружает файл в формате excel в MDS.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.OfflineReportJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'span_id~'log_level~'message)~conditions~(service~'direct.jobs~method~'offlinereport.OfflineReportJob)~limit~1000~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Отчеты этого типа перестанут строиться.


### Как пользователи (или команда) заметят проблему и через какое время

Отчёт в интерфейсе будет ждать построения.


### Контакты разработчиков и менеджеров

Разработчики: [Андрей Павленко](https://staff.yandex-team.ru/andreypav) <br/>
Менеджеры: [Дмитрий Лянге](https://staff.yandex-team.ru/)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

Отсутствуют


### Известные причины поломок

Если `Hahn` недоступен, то отчёт построится, когда кластер вернётся в строй.


### Дополнительно: тонкости и подводные камни

Отчёт не актуален в середине квартала.
Таблицы Биллинга не доступны разработчикам директа, доступны только роботу.
