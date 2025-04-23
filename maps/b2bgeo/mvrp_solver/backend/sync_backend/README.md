# B2Bgeo Syncsolver

Synchronous VRP solver

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [abc:maps-b2bgeo-syncsolver](https://abc.yandex-team.ru/services/maps-b2bgeo-syncsolver/) |
| Отвественные SRE | Elena Markova (4c4d@yandex-team.ru) |
| Исходники | [maps/b2bgeo/mvrp_solver/backend/sync_backend](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/mvrp_solver/backend/sync_backend) |
| Сервис в ABC | [maps-b2bgeo-syncsolver](https://abc.yandex-team.ru/services/maps-b2bgeo-syncsolver/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_B2BGEO_SYNCSOLVER |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stress | [maps_b2bgeo_syncsolver_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_stress/) | [ b2bgeo-syncsolver.stress ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-syncsolver-stress-panel-main/) | [ maps_b2bgeo_syncsolver_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_syncsolver_stress) |
| Testing | [maps_b2bgeo_syncsolver_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_testing/) | [ b2bgeo-syncsolver.testing ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-syncsolver-testing-panel-main/) | [ maps_b2bgeo_syncsolver_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_syncsolver_testing) |
| Prestable | [maps_b2bgeo_syncsolver_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_prestable/) | [ b2bgeo-syncsolver.prestable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-syncsolver-prestable-panel-main/) | [ maps_b2bgeo_syncsolver_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_syncsolver_prestable) |
| Stable | [maps_b2bgeo_syncsolver_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_stable/) | [ b2bgeo-syncsolver.stable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-syncsolver-stable-panel-main/) | [ maps_b2bgeo_syncsolver_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_syncsolver_stable) |


[Monitorings all (tag=a_prj_maps-b2bgeo-syncsolver)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-b2bgeo-syncsolver)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Testing | Default | [b2bgeo-syncsolver.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-syncsolver.testing.maps.yandex.net/) | [b2bgeo-syncsolver.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=b2bgeo-syncsolver.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man;prj=b2bgeo-syncsolver-testing-maps;signal=service_total) | [rtc_balancer_b2bgeo-syncsolver_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-syncsolver_testing_maps_yandex_net_man)<br>[rtc_balancer_b2bgeo-syncsolver_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-syncsolver_testing_maps_yandex_net_sas) |
| Stable | Default | [b2bgeo-syncsolver.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-syncsolver.maps.yandex.net/) | [b2bgeo-syncsolver.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=b2bgeo-syncsolver.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man,vla;prj=b2bgeo-syncsolver-maps;signal=service_total) | [rtc_balancer_b2bgeo-syncsolver_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-syncsolver_maps_yandex_net_man)<br>[rtc_balancer_b2bgeo-syncsolver_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-syncsolver_maps_yandex_net_sas)<br>[rtc_balancer_b2bgeo-syncsolver_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-syncsolver_maps_yandex_net_vla)


## What happens when service is down

When service is down VRP tasks cannot be solved in synchronous mode, YCB is not able to update `route_state` and ETA for all imported routes.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/sync-solver/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Access log (YT) | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`logs/maps-log/1d/2021-01-15` WHERE vhost LIKE 'b2bgeo-syncsolver.maps.yandex.net' limit 1;``` |
| Yacare service (YT; testing) | https://yt.yandex-team.ru/hahn/navigation?path=//logs/b2bgeo-syncsolver-testing-log |
| Yacare service (YT; stable) | https://yt.yandex-team.ru/hahn/navigation?path=//logs/b2bgeo-syncsolver-stable-log |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

[B2Bgeo Troubleshooting](https://wiki.yandex-team.ru/b2bgeo/dev/helpdesk/troubleshooting/)

## Documentation

https://wiki.yandex-team.ru/b2bgeo/dev/vrs/

## Known clients
- YCB: [calculate eta](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/backend/ya_courier_backend/logic/eta.py?rev=r7756744#L201), [update route state](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/backend/ya_courier_backend/tasks/update_route_state.py?rev=r7756744#L379)
- БЯК: [optimize route](https://yandex.ru/maps/-/CCQlnOtoDD)



## SLA
TBD


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_stress/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_syncsolver_stable/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_B2BGEO_SYNCSOLVER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_SYNCSOLVER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_B2BGEO_SYNCSOLVER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_SYNCSOLVER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
TBD
