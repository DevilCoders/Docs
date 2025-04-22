# B2Bgeo Asyncsolver

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [abc:maps-b2bgeo-asyncsolver](https://abc.yandex-team.ru/services/maps-b2bgeo-asyncsolver/) |
| Отвественные SRE | Elena Markova (4c4d@yandex-team.ru) |
| Исходники | [maps/b2bgeo/mvrp_solver/backend/async_backend](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/mvrp_solver/backend/async_backend) |
| Сервис в ABC | [maps-b2bgeo-asyncsolver](https://abc.yandex-team.ru/services/maps-b2bgeo-asyncsolver/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_B2BGEO_ASYNCSOLVER |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stress | [maps_b2bgeo_asyncsolver_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_stress/) | [ b2bgeo-asyncsolver.stress ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-asyncsolver-stress-panel-main/) | [ maps_b2bgeo_asyncsolver_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_asyncsolver_stress) |
| Testing | [maps_b2bgeo_asyncsolver_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_testing/) | [ b2bgeo-asyncsolver.testing ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-asyncsolver-testing-panel-main/) | [ maps_b2bgeo_asyncsolver_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_asyncsolver_testing) |
| Stable | [maps_b2bgeo_asyncsolver_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_stable/) | [ b2bgeo-asyncsolver.stable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-asyncsolver-stable-panel-main/) | [ maps_b2bgeo_asyncsolver_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_asyncsolver_stable) |
| Prestable | [maps_b2bgeo_asyncsolver_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_prestable/) | [ b2bgeo-asyncsolver.prestable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-asyncsolver-prestable-panel-main/) | [ maps_b2bgeo_asyncsolver_prestable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_asyncsolver_prestable) |


[Monitorings all (tag=a_prj_maps-b2bgeo-asyncsolver)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-b2bgeo-asyncsolver)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Testing | Default | [b2bgeo-asyncsolver.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-asyncsolver.testing.maps.yandex.net/) | [b2bgeo-asyncsolver.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=b2bgeo-asyncsolver.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas;prj=b2bgeo-asyncsolver-testing-maps;signal=service_total) | [rtc_balancer_b2bgeo-asyncsolver_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-asyncsolver_testing_maps_yandex_net_man)<br>[rtc_balancer_b2bgeo-asyncsolver_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-asyncsolver_testing_maps_yandex_net_sas) |
| Stable | Default | [b2bgeo-asyncsolver.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-asyncsolver.maps.yandex.net/) | [b2bgeo-asyncsolver.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=b2bgeo-asyncsolver.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=b2bgeo-asyncsolver-maps;signal=service_total) | [rtc_balancer_b2bgeo-asyncsolver_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-asyncsolver_maps_yandex_net_man/)<br>[rtc_balancer_b2bgeo-asyncsolver_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-asyncsolver_maps_yandex_net_sas/)<br>[rtc_balancer_b2bgeo-asyncsolver_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-asyncsolver_maps_yandex_net_vla/) |


## What happens when service is down

When service is down VRS API doesn't work, routes planning is unavailable.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/async-solver/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Access log (YT) | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'b2bgeo-asyncsolver.maps.yandex.net' limit 1;``` |
| Yacare service (YT; testing) | https://yt.yandex-team.ru/hahn/navigation?path=//logs/b2bgeo-asyncsolver-testing-log |
| Yacare service (YT; stable) | https://yt.yandex-team.ru/hahn/navigation?path=//logs/b2bgeo-asyncsolver-stable-log |

## Integration tests

Tests run as acceptance after releasing the service to testing or stable using sedem.

[More info](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/mvrp_solver/backend/integration_tests/README.md).

## Rerun failed tasks

Sandbox task from template [MAPS_B2BGEO_SOLVER_INTEGRATION_TEST_TEMPLATE_TESTING](https://sandbox.yandex-team.ru/template/MAPS_B2BGEO_SOLVER_INTEGRATION_TEST_TEMPLATE_TESTING/view) reruns last failed solver tasks as an acceptance test after release to testing.

[More info](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/mvrp_solver/backend/tools/rerun_failed_tasks/README.md)

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
[Troubleshooting](https://wiki.yandex-team.ru/b2bgeo/dev/helpdesk/troubleshooting/)

## Documentation

https://wiki.yandex-team.ru/b2bgeo/dev/vrs/

## Known clients
- YCB: [Proxy to VRS API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/backend/ya_courier_backend/resources/mvrp.py)


## SLA
TBD


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log
* /persistent - файлы с матрицами для отправки на YT

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_stress/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_asyncsolver_stable/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_B2BGEO_ASYNCSOLVER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_ASYNCSOLVER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_B2BGEO_ASYNCSOLVER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_ASYNCSOLVER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
TBD
