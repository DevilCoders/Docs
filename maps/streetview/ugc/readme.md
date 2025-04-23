# Core Stv Ugc

<< Сервис приёма поставок панорам от поставщиков и пользователей. Внешняя торчащая наружу часть бэкофиса панорам >>
## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Отвественные SRE | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Исходники | [maps/streetview/ugc](https://a.yandex-team.ru/arc/trunk/arcadia/maps/streetview/ugc) |
| Сервис в ABC | [maps-core-stv-ugc](https://abc.yandex-team.ru/services/maps-core-stv-ugc/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_STV_UGC |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_stv_ugc_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_ugc_stable/) | [ core-stv-ugc.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-stv-ugc-stable-panel-main/) | [ maps_core_stv_ugc_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_stv_ugc_stable) |
| Testing | [maps_core_stv_ugc_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_ugc_testing/) | [ core-stv-ugc.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-stv-ugc-testing-panel-main/) | [ maps_core_stv_ugc_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_stv_ugc_testing) |


[Monitorings all (tag=a_prj_maps-core-stv-ugc)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-stv-ugc)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-stv-ugc.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-stv-ugc.maps.yandex.net/) | [core-stv-ugc.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-stv-ugc.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,man,sas;prj=core-stv-ugc-maps;signal=service_total) | [rtc_balancer_core-stv-ugc_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stv-ugc_maps_yandex_net_man)<br>[rtc_balancer_core-stv-ugc_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stv-ugc_maps_yandex_net_sas)<br>[rtc_balancer_core-stv-ugc_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stv-ugc_maps_yandex_net_vla) |
| Testing | Default | [core-stv-ugc.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-stv-ugc.testing.maps.yandex.net/) | [core-stv-ugc.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-stv-ugc.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-stv-ugc-testing-maps;signal=service_total) | [rtc_balancer_core-stv-ugc_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-stv-ugc_testing_maps_yandex_net_sas) |


## What happens when service is down
Внешние поставики не могут загружать панорамы. Не могут видеть свои уже загруженные поставки, отправлять их на модерацию.


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-stv-ugc.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Убедиться что все впорядке с базой
https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=22a02a84-18a4-41d4-8140-56b3e20d443a;dbname=streetview_ugc


## Documentation

https://wiki.yandex-team.ru/users/orphean/stv-ugc/
https://a.yandex-team.ru/arc/trunk/arcadia/maps/streetview/ugc/yacare/readme.md


## Known clients
Сервис для публикации пользовательских панорам
https://qloud-ext.yandex-team.ru/projects/maps/front-pano-ugc?tab=access

Продакшен урл
https://pano.maps.yandex.ru

Тестинг урл
https://pano.tst.c.maps.yandex.ru


## SLA
## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_stv_ugc) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_stv_ugc.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods
| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_ugc_testing/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_ugc_prestable/ |
| Production | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_ugc_stable/ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_ugc_load/ |

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_STV_UGC_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STV_UGC_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_STV_UGC_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STV_UGC_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSPANO
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/22571
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/22570
    * Тикет: https://st.yandex-team.ru/MAPSPANO-577


