# Auto Remote Tasks Scheduler

Service, which communicates with users, adds their tasks to Startrek and PgaaS, and checks access permissions

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Крутяков (mkrutyakov@yandex-team.ru) |
| Отвественные SRE | Михаил Крутяков (mkrutyakov@yandex-team.ru), Михаил Куприянов (kupriyanov-m@yandex-team.ru) |
| Исходники | [maps/automotive/remote_tasks/scheduler](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/remote_tasks/scheduler) |
| Сервис в ABC | [maps-auto-remote-tasks-scheduler](https://abc.yandex-team.ru/services/maps-auto-remote-tasks-scheduler/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_REMOTE_TASKS_SCHEDULER |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_auto_remote_tasks_scheduler_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_prestable/) | [ auto-remote-tasks-scheduler.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-scheduler-prestable-panel-main/) | [ maps_auto_remote_tasks_scheduler_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_scheduler_prestable) |
| Stable | [maps_auto_remote_tasks_scheduler_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_stable/) | [ auto-remote-tasks-scheduler.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-scheduler-stable-panel-main/) | [ maps_auto_remote_tasks_scheduler_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_scheduler_stable) |
| Stress | [maps_auto_remote_tasks_scheduler_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_stress/) | [ auto-remote-tasks-scheduler.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-scheduler-stress-panel-main/) | [ maps_auto_remote_tasks_scheduler_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_scheduler_stress) |
| Testing | [maps_auto_remote_tasks_scheduler_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_testing/) | [ auto-remote-tasks-scheduler.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-scheduler-testing-panel-main/) | [ maps_auto_remote_tasks_scheduler_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_scheduler_testing) |


[Monitorings all (tag=a_prj_maps-auto-remote-tasks-scheduler)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-remote-tasks-scheduler)

**Ratelimiter panel:** [RPS and Quotas](https://yasm.yandex-team.ru/template/panel/maps_auto_remote_tasks-ratelimiter2-panel/)

**S3 monitorings**

| Staging | Graphics panel for bucket |
| ------- | -------------- |
| Stable | [maps-auto-remote-tasks-reports](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-auto-remote-tasks-reports;owner=31505) |
| Testing | [maps-auto-remote-tasks-reports](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-auto-remote-tasks-reports;owner=31505;ctype=testing) |

**MDB monitorings**

| Staging | Graphics panel |
| ------- | -------------- |
| Stable | [maps-auto-remote-tasks-stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb0suuk1cfvbl3hskln) |
| Testing | [maps-auto-remote-tasks-testing](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbi6vu9v3dp28e1fhu2) |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [auto-remote-tasks-scheduler.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-remote-tasks-scheduler.maps.yandex.net/) | [auto-remote-tasks-scheduler.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-remote-tasks-scheduler.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=auto-remote-tasks-scheduler-maps;signal=service_total) | [rtc_balancer_auto-remote-tasks-scheduler_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-tasks-scheduler_maps_yandex_net_man)<br>[rtc_balancer_auto-remote-tasks-scheduler_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-tasks-scheduler_maps_yandex_net_sas)<br>[rtc_balancer_auto-remote-tasks-scheduler_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-tasks-scheduler_maps_yandex_net_vla) |

### Other components

| Name | Testing | Stable |
| ---- | ------- | ------ |
| Форма для запроса баг-репортов | [Заказ багрепорта для ГУ (тест)](https://forms.test.yandex-team.ru/admin/6787/) | [Заказ багрепорта для ГУ](https://forms.yandex-team.ru/admin/50268/) |
| Очередь в Startrek | https://st.test.yandex-team.ru/AUTOREPORT | https://st.yandex-team.ru/AUTOREPORT |
| Сервис в IDM | [Планировщик задач ГУ (тест)](https://idm.test.yandex-team.ru/system/maps-auto-remote-tasks-test) | [Планировщик задач ГУ](https://idm.yandex-team.ru/system/maps-auto-remote-tasks) |
| Startrek Secret | [maps-auto-testing-remote-tasks-startrek](https://yav.yandex-team.ru/secret/sec-01efhqtw4sav68nfnsam2s7sx5/explore/versions) | [maps-auto-stable-remote-tasks-startrek](https://yav.yandex-team.ru/secret/sec-01efhrd3npkwz0f87zsd2psrj6/explore/versions) |
| PostgreSQL | [maps-auto-remote-tasks-testing](https://yc.yandex-team.ru/folders/foopuat55bs8o28pa0cv/managed-postgresql/cluster/mdbi6vu9v3dp28e1fhu2) | [maps-auto-remote-tasks-stable](https://yc.yandex-team.ru/folders/foopuat55bs8o28pa0cv/managed-postgresql/cluster/mdb0suuk1cfvbl3hskln) |
| S3 Service account / Bucket | Выполнение задач на ГУ (S3 Testing) | Выполнение задач на ГУ |


## What happens when service is down

Пользователи репортов Яндекс.Авто не могут запрашивать багрепорты с ГУ. Недоступно скачивание багрепортов по ссылке. Перестаёт работать синхронизация статуса сбора багрепорта со Startrek. Ломается запрос ролей в системе через IDM.


## BlackBox grants

Search for maps-auto-remote-tasks in this [form](https://grantushka.yandex-team.ru/grants/consumer/).
Generaly this service uses BlackBox grants to determine user login by cookie.
Yandex-Team BlackBox is used here because we work with internal users only (@yandex-team.ru).

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-remote-tasks-scheduler/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'auto-remote-tasks-scheduler.maps.yandex-team.ru' limit 1; |

## How to fix common problems

* [Ratelimiter alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2/agent_troubleshooting.md)
* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
* **IDM**. В случае неполадок с доступами имеет смысл проверить статус сервиса через интерфейс IDM (сначала на вкладке **Синхронизация** нажать кнопку **Запустить сверку**, затем во вкладке **Расхождения** проверить результат).
* **total-404** Это может быть **crasher** или **molly** (утилиты СИБа). Проверяется по наличию параметра `everybodybecoolthisis=crasher` или `everybodybecoolthisis=molly` в запросе.

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

- [Дизайн-ревью](https://wiki.yandex-team.ru/Automotive/serverdevelopment/logs-collection/second-design-review/)
- [Инструкция для пользователей системы](https://wiki.yandex-team.ru/automotive/serverdevelopment/logs-collection/guide-for-dev-with-startrek)

## Known clients

- IDM
- Startrek (триггер при заведении задачи на запрос багрепорта)

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_stable/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_scheduler_stress/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_REMOTE_TASKS_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_REMOTE_TASKS_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_REMOTE_TASKS_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_REMOTE_TASKS_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/YCARBACKEND?service=maps-auto-remote-tasks-manager
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/YCARBACKEND-566

