# Core Garden Server

Бэкенд Огорода. Предоставляет API, в которое ходят UI Огорода и другие сервисы.

Через API можно получать информацию о сборке данных в Огороде и выполнять различные операции.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Александр Бобков (alexbobkov@yandex-team.ru) |
| Отвественные SRE | Александр Бобков (alexbobkov@yandex-team.ru) |
| Исходники | [maps/garden/server](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/server) |
| Сервис в ABC | [maps-core-garden](https://abc.yandex-team.ru/services/maps-core-garden/)|
| CI | https://a.yandex-team.ru/projects/maps-core-garden/ci/actions/launches?dir=maps/garden/server&id=build |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_garden_server_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_garden_server_stable/) | [ core-garden-server.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-garden-server-stable-panel-main/) | [ maps_core_garden_server_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_garden_server_stable) |
| Testing | [maps_core_garden_server_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_garden_server_testing/) | [ core-garden-server.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-garden-server-testing-panel-main/) | [ maps_core_garden_server_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_garden_server_testing) |

[Monitorings all (tag=a_prj_maps-core-garden-server)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-garden-server)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-garden-server.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-garden-server.maps.yandex.net/) | [core-garden-server.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-garden-server.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-garden-server-maps;signal=service_total) | [rtc_balancer_core-garden-server_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-garden-server_maps_yandex_net_man)<br>[rtc_balancer_core-garden-server_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-garden-server_maps_yandex_net_sas)<br>[rtc_balancer_core-garden-server_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-garden-server_maps_yandex_net_vla) |


### MDB Mongo clusters

| Staging | MDB cluster |
| ------- | ----------- |
| stable | [cluster](https://yc.yandex-team.ru/folders/fooj6ecqh8rsdsnj5806/managed-mongodb/cluster/mdbgovfcc6lo1thpd2ke) |
| testing | [cluster](https://yc.yandex-team.ru/folders/fooj6ecqh8rsdsnj5806/managed-mongodb/cluster/mdbj0vjs787pnuhr77s2) |


### BB grants

| Staging | Grants |
| ------- | ----------- |
| stable | [grantushka](https://grantushka.yandex-team.ru/grants/issue/28689/) |
| testing | [grantushka](https://grantushka.yandex-team.ru/grants/issue/28687/) |


## Доступ

Для доступа к Огороду на чтение нужно быть членом [ABC-сервиса](https://abc.yandex-team.ru/services/maps-core-garden-users/).

Права на операции в Огороде можно запросить в [IDM](https://idm.yandex-team.ru/system/garden_roles/roles#rf=1,f-status=all,f-role=garden_roles,sort-by=-updated,rf-expanded=f8H5DQu2,rf-role=f8H5DQu2#garden_roles(fields:())).


## What happens when service is down

UI Огорода не работает. Как следствие, невозможно узнать, что происходит в Огороде, невозможно запускать, отменять билды, откатывать релизы данных.

Шедьюлер Огорода живёт в другом сервисе, поэтому в теории при отказе бэкенда Огорода шедьюлер будет продолжать работать.


## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2021-07-01` WHERE tskv_format="garden-server" limit 1; |
| Garden | /var/log/yandex/maps/garden/* |


## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

[Инструкция в документации Огорода](https://docs.yandex-team.ru/garden/garden_duty)


## Documentation

[Документация](https://docs.yandex-team.ru/garden/)


## Known clients

* [Garden UI](https://yd.yandex-team.ru/stages/maps-front-garden_production)
* [Garden CLI](https://docs.yandex-team.ru/garden/cli)
* [GARDEN_UPLOAD_MODULE_BINARY](https://sandbox.yandex-team.ru/tasks?children=true&type=GARDEN_UPLOAD_MODULE_BINARY&hidden=true&limit=20)
* [Sedem](https://docs.yandex-team.ru/sedem/)
* [stylerepo](https://abc.yandex-team.ru/services/maps-core-renderer-stylerepo)
* [indoor](https://abc.yandex-team.ru/services/maps-core-indoor-radiomap-capturer)
* [nmaps publication_check_worker](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_realtime/src/publication_check_worker)


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_garden_server)

[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_garden_server.py)


## Persistent Volumes

* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_GARDEN_SERVER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GARDEN_SERVER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_GARDEN_SERVER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_GARDEN_SERVER_TESTING_RTC_NETS_ ) |
