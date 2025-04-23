# Maps-Core-Gpstiles
Service for rendering aggregated GPS tracks from users.

## General information

| | |
|---|---|
| Maintainers | https://staff.yandex-team.ru/quoter |
| SRE |   |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/gpstiles |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_GPSTILES |
| ABC | https://abc.yandex-team.ru/services/maps-core-gpstiles/ |
| Tracker queue | https://st.yandex-team.ru/NMAPS |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_gpstiles_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_gpstiles_stable/) | [ core-gpstiles.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-gpstiles-stable-panel-main/) | [ maps_core_gpstiles_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpstiles_stable) |
| Testing | [maps_core_gpstiles_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_gpstiles_testing/) | [ core-gpstiles.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-gpstiles-testing-panel-main/) | [ maps_core_gpstiles_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpstiles_testing) |


[Monitorings all (tag=a_prj_maps-core-gpstiles)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-gpstiles)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-gpstiles.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-gpstiles.maps.yandex.net/) | [core-gpstiles.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-gpstiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-gpstiles-maps;signal=service_total) | [rtc_balancer_core-gpstiles_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-gpstiles_maps_yandex_net_man)<br>[rtc_balancer_core-gpstiles_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-gpstiles_maps_yandex_net_sas)<br>[rtc_balancer_core-gpstiles_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-gpstiles_maps_yandex_net_vla) |

## How to test service
Open url in browser.

| Environment | URL |
|---|---|
| stable | https://core-gpstiles.maps.yandex.net/tiles?style=point&x=4949&y=2569&z=13 |
| testing | https://core-gpstiles.testing.maps.n.yandex.ru/tiles?style=point&x=9561&y=4808&z=14 |

## Documentation

[Документация устарела](https://wiki.yandex-team.ru/maps/dev/core/factory/signals_update/)

## Known clients

- НЯК - агрегированные треки показываются отдельным слоем.
- Фабрика - агрегированные треки показываются отдельным слоем.
- Урлы используются для подгрузки тайловых слоев в интерфейсах, которые это позволяют (фабрика, mpro). [Список урлов, которыми пользуются картографы](https://wiki.yandex-team.ru/users/kgolenkova/ssylki-dlja-podgruzki-v-redaktor/).

## What happens when service is down

- в НЯК не виден слой GPS-треки
- не видны слои треков на Фабрике
- не виден вручную подключенный слой в mpro

Частичные деградации не предусмотрены

## How to fix common problems

Проверить, что запущен yacare
ps aux | grep yacare | grep gpstiles

Посмотреть, что бакет s3mds отвечает адекватно.

## SLA

TBD: более понятно будет после [стрельбы](https://st.yandex-team.ru/NMAPS-7676)

## Monitorings

| Name | URL |
|---|---|
| Juggler stable (by sedem) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpstiles_stable&view=tiles |
| Juggler testing (by sedem) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_gpstiles_testing&view=tiles |

## Dashboards

| Name | URL |
|---|---|
| stable (by sedem) | https://yasm.yandex-team.ru/template/panel/maps-core-gpstiles-stable-panel-main |
| testing (by sedem) | https://yasm.yandex-team.ru/template/panel/maps-core-gpstiles-testing-panel-main |
| s3 bucket stable | https://yasm.yandex-team.ru/panel/s3_client;bucket=maps-gpstiles;owner=1971?range=604800000 |
| s3 bucket testing | https://yasm.yandex-team.ru/panel/s3_client;bucket=maps-gpstiles-testing;owner=1971?range=604800000 |
| DBaas stable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbclgtnv1p53a9rvg9t;dbname=mapsfactory_signals |
| DBaas testing | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb7dc18bcuk50vfkk45;dbname=mapsfactory_signals_test |

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/access.log |
| yacare gpstiles | /var/log/yandex/maps/gpstiles/gpstiles.log |

## Regression Stress Testing Configurations

[TBD](https://st.yandex-team.ru/NMAPS-7676)
