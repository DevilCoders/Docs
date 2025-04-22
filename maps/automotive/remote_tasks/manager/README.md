# Auto Remote Tasks Manager

Service, which communicates with a head unit, sends new tasks to it, receives and dispatches their results

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Крутяков (mkrutyakov@yandex-team.ru) |
| Отвественные SRE | Михаил Крутяков (mkrutyakov@yandex-team.ru), Михаил Куприянов (kupriyanov-m@yandex-team.ru) |
| Исходники | [maps/automotive/remote_tasks/manager](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/remote_tasks/manager) |
| Сервис в ABC | [maps-auto-remote-tasks-manager](https://abc.yandex-team.ru/services/maps-auto-remote-tasks-manager/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_REMOTE_TASKS_MANAGER |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_auto_remote_tasks_manager_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_prestable/) | [ auto-remote-tasks-manager.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-manager-prestable-panel-main/) | [ maps_auto_remote_tasks_manager_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_manager_prestable) |
| Stable | [maps_auto_remote_tasks_manager_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_stable/) | [ auto-remote-tasks-manager.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-manager-stable-panel-main/) | [ maps_auto_remote_tasks_manager_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_manager_stable) |
| Stress | [maps_auto_remote_tasks_manager_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_stress/) | [ auto-remote-tasks-manager.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-manager-stress-panel-main/) | [ maps_auto_remote_tasks_manager_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_manager_stress) |
| Testing | [maps_auto_remote_tasks_manager_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_testing/) | [ auto-remote-tasks-manager.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-remote-tasks-manager-testing-panel-main/) | [ maps_auto_remote_tasks_manager_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_remote_tasks_manager_testing) |


[Monitorings all (tag=a_prj_maps-auto-remote-tasks-manager)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-remote-tasks-manager)

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
| Stable | Default | [auto-remote-tasks-manager.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-remote-tasks-manager.maps.yandex.net/) | [auto-remote-tasks-manager.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-remote-tasks-manager.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=auto-remote-tasks-manager-maps;signal=service_total) | [rtc_balancer_auto-remote-tasks-manager_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-tasks-manager_maps_yandex_net_man)<br>[rtc_balancer_auto-remote-tasks-manager_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-tasks-manager_maps_yandex_net_sas)<br>[rtc_balancer_auto-remote-tasks-manager_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-remote-tasks-manager_maps_yandex_net_vla) |

### Other components

| Name | Testing | Stable |
| ---- | ------- | ------ |
| PostgreSQL | [maps-auto-remote-tasks-testing](https://yc.yandex-team.ru/folders/foopuat55bs8o28pa0cv/managed-postgresql/cluster/mdbi6vu9v3dp28e1fhu2) | [maps-auto-remote-tasks-stable](https://yc.yandex-team.ru/folders/foopuat55bs8o28pa0cv/managed-postgresql/cluster/mdb0suuk1cfvbl3hskln) |
| S3 Service account / Bucket | Выполнение задач на ГУ (S3 Testing) | Выполнение задач на ГУ |


## What happens when service is down

Головные устройства Яндекс.Авто не могут получить информацию о запросах на получение багрепортов. Также они больше не могут отправлять багрепорты.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-remote-tasks-manager/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'auto-remote-tasks-manager.maps.yandex.net' limit 1; |

## How to fix common problems

* [Ratelimiter alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2/agent_troubleshooting.md)
* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
* **total-404** Это может быть **crasher** или **molly** (утилиты СИБа). Проверяется по наличию параметра `everybodybecoolthisis=crasher` или `everybodybecoolthisis=molly` в запросе.

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

- [Дизайн-ревью](https://wiki.yandex-team.ru/Automotive/serverdevelopment/logs-collection/second-design-review/)

## Known clients

- Аппа по отправке багрепортов Яндекс.Авто

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
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_stable/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_remote_tasks_manager_stress/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_REMOTE_TASKS_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_REMOTE_TASKS_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_REMOTE_TASKS_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_REMOTE_TASKS_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/YCARBACKEND?service=maps-auto-remote-tasks-manager
    * Sandbox (line): https://sandbox.yandex-team.ru/scheduler/24147
    * Sandbox (const): https://sandbox.yandex-team.ru/scheduler/24148
    * Sandbox (line, is_alive): https://sandbox.yandex-team.ru/scheduler/25561/view
    * Sandbox (const, is_alive): https://sandbox.yandex-team.ru/scheduler/25563/view
    * Тикет: https://st.yandex-team.ru/YCARBACKEND-566

## S3 Setup Instructions

Чтобы багрепорты удалялись по истечении заданного периода времени, необходимо выполнить настройку Lifecycle для бакета в S3 следующим образом:

```
# Задаём настройки удаления файлов через 180 дней:
aws --endpoint-url=https://s3.mds.yandex.net \
    s3api put-bucket-lifecycle-configuration \
    --bucket maps-auto-remote-tasks-reports \
    --lifecycle-configuration '{
    "Rules": [
        {
            "ID": "DeleteOldUploads",
            "Status": "Enabled",
            "Filter": {
                "Prefix": ""
            },
            "Expiration": {
                "Days": 180
            }
        }
    ]
}'

# Проверка, что настройки загрузились:
aws --endpoint-url=https://s3.mds.yandex.net \
    s3api get-bucket-lifecycle-configuration \
    --bucket maps-auto-remote-tasks-reports
```

