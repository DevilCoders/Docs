# Core Nmaps Tasks

Wiki-tasks: управление длинными задачами Народной Карты

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Борис Чикунов (chikunov@yandex-team.ru) <br> Алексей Пономарев (ponomarev@yandex-team.ru) <br> Илья Власюк (tail@yandex-team.ru) |
| Отвественные SRE | Борис Чикунов (chikunov@yandex-team.ru) <br> Алексей Пономарев (ponomarev@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/tasks/fastcgi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks/fastcgi) |
| Сервис в ABC | [maps-core-nmaps-tasks](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks/)|
| Проект в CI | [maps-core-nmaps-tasks](https://a.yandex-team.ru/projects/maps-core-nmaps-tasks/ci/actions/launches?dir=maps/wikimap/mapspro/services/tasks/fastcgi) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_tasks_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_stable/) | [ core-nmaps-tasks.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-stable-panel-main/) | [ maps_core_nmaps_tasks_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_stable) |
| Testing | [maps_core_nmaps_tasks_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_testing/) | [ core-nmaps-tasks.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-testing-panel-main/) | [ maps_core_nmaps_tasks_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_testing) |
| Unstable | [maps_core_nmaps_tasks_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_unstable/) | [ core-nmaps-tasks.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-unstable-panel-main/) | [ maps_core_nmaps_tasks_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_tasks_unstable) |


[Monitorings all (tag=a_prj_maps-core-nmaps-tasks)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-tasks)

| Staging | User panels |
| ------- | ----------- |
| Stable | https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-stable-panel-main/ |
| Testing | https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-testing-panel-main/ |
| Unstable | https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-tasks-unstable-panel-main/ |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-tasks.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-tasks.maps.yandex.net/) | [core-nmaps-tasks.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-tasks.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,msk;prj=core-nmaps-tasks-maps;signal=service_total) | [rtc_balancer_core-nmaps-tasks_maps_yandex_net_myt](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-tasks_maps_yandex_net_myt)<br>[rtc_balancer_core-nmaps-tasks_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-tasks_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-tasks_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-tasks_maps_yandex_net_vla) |
| Testing | Default | [core-nmaps-tasks.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-tasks.testing.maps.yandex.net/) | [core-nmaps-tasks.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-tasks.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-nmaps-tasks-testing-maps;signal=service_total) | [rtc_balancer_core-nmaps-tasks_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-tasks_testing_maps_yandex_net_sas) |
| Unstable | Default | [core-nmaps-tasks.unstable.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-tasks.unstable.maps.yandex.net/) | [core-nmaps-tasks.unstable.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-tasks.unstable.maps.yandex.net;itype=balancer;ctype=prod;locations=vla;prj=core-nmaps-tasks-unstable-maps;signal=service_total) | [rtc_balancer_core-nmaps-tasks_unstable_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-tasks_unstable_maps_yandex_net_vla) |


## What happens when service is down

Теряется возможность управлять длинными задачами в Народной Карте - запуск, просмотр, редактирование расписания и т. п.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Fastcgi | /var/log/yandex/maps/wiki/tasks/fastcgi/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-nmaps-tasks.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

[Документация в Wiki](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/tasks/)

## Known clients
- Морда mpro (Единая Карта)

## SLA

N/A

## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_testing/yp_pods/ |
| Unstable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_unstable/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_TASKS_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_TASKS_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_TASKS_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_TASKS_TESTING_RTC_NETS_ ) |
| unstable | [ \_MAPS_CORE_NMAPS_TASKS_UNSTABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_TASKS_UNSTABLE_RTC_NETS_ ) |

## Regression Stress Testing Configurations
N/A. Сервис малой и разношёрстной нагрузки.
