## CampQueueMonitoringJob

### Продукт/подсистема

Копирование кампаний.


### Роль в работе продукта/подсистемы

- Мониторит возраст очереди копирования.
- Отправляет в Solomon метрики:
  - возраст очереди копирования;
  - размер очереди;
  - количество уникальных клиентов в очереди.


### Датафлоу

- Делает селекты в [ppc.camp_operations_queue_copy](https://direct-dev.yandex-team.ru/db/ppc/tables/camp_operations_queue_copy.html) для получения вышеуказанных метрик и отправляет их в Solomon.
- Если возраст очереди превышает значение ppc-property `camp_operations_queue_copy_age_limit_hours`, то зажигает свою лампочку в Juggler.


### Способы наблюдения за текущим состоянием

- [Возраст очереди](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java_jobs&l.sensor=age_minutes&l.host=CLUSTER&graph=auto&l.queue=camp_operations_queue_copy&l.env=production&stack=false)
- [Размер очереди](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java_jobs&l.sensor=queue_size&l.host=CLUSTER&graph=auto&l.queue=camp_operations_queue_copy&l.env=production&stack=false)
- [Количество ожидающих клиентов](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java_jobs&l.sensor=clients_waiting&l.host=CLUSTER&graph=auto&l.queue=camp_operations_queue_copy&l.env=production&stack=false)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CampQueueMonitoringJob.working.production&query=&last=1MONTH)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'campqueue.CampQueueMonitoringJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Когда загорается лампочка - значит, возраст очереди превышает лимит, нужно смотреть на копирование кампаний, а это критично.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи будут долго ждать, пока их кампании скопируются.


### Контакты разработчиков и менеджеров

Разработчики:
- [Александр Дубинкин](https://staff.yandex-team.ru/adubinkin) - непосредственно копирование в Perl
- [Сергей Белоусов](https://staff.yandex-team.ru/mexicano) - данная мониторинговая джоба


### Желательное время исправления в случае поломки

Копирование кампаний чинить asap. Многие пользователи создают рекламу через копирование, и оно должно быть быстрым.


### Способы регулирования работы джобы

- Ppc-property `camp_operations_queue_copy_age_limit_hours` отвечает за лимит возраста очереди в часах. На момент написания лимит равен 4м часам.


### Известные причины поломок

- Возраст очереди превышает лимит.


### Дополнительно: тонкости и подводные камни

- [Документация перлового скрипта копирования кампаний ppcCampQueue.pl](../../perl-scripts/list/ppcCampQueue.pl)
