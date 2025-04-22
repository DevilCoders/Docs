# B2Bgeo Routing Public Api

Service provides Routing public API functionality according to documentation: https://tech.yandex.ru/routing/router/doc/concepts/about-docpage/

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Elena Markova (4c4d@yandex-team.ru) |
| Отвественные SRE | Anton Gorokhov (gorokhov@yandex-team.ru), Dmitry Tyo (dtyo@yandex-team.ru) |
| Исходники | [maps/b2bgeo/routing_public_api](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/routing_public_api) |
| Сервис в ABC | [maps-b2bgeo-routing-public-api](https://abc.yandex-team.ru/services/maps-b2bgeo-routing-public-api/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_B2BGEO_ROUTING_PUBLIC_API |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_b2bgeo_routing_public_api_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routing_public_api_stable/) | [ b2bgeo-routing-public-api.stable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-routing-public-api-stable-panel-main/) | [ maps_b2bgeo_routing_public_api_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_routing_public_api_stable) |
| Testing | [maps_b2bgeo_routing_public_api_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routing_public_api_testing/) | [ b2bgeo-routing-public-api.testing ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-routing-public-api-testing-panel-main/) | [ maps_b2bgeo_routing_public_api_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_routing_public_api_testing) |


[Monitorings all (tag=a_prj_maps-b2bgeo-routing-public-api)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-b2bgeo-routing-public-api)

| Staging | User panels |
| ------- | ----------- |
| Stable | https://yasm.yandex-team.ru/template/panel/b2b_routing_public_api_sedem/env=stable/ |
| Testing | https://yasm.yandex-team.ru/template/panel/b2b_routing_public_api_sedem/env=testing/ |


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/routing_public_api/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`logs/maps-log/1d/2020-07-20` WHERE vhost LIKE 'api.routing.yandex.net' limit 1;``` |


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


## Documentation

https://wiki.yandex-team.ru/b2bgeo/dev/routing_public_api/
https://tech.yandex.ru/routing/router/doc/concepts/about-docpage/


## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routing_public_api_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routing_public_api_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_B2BGEO_ROUTING_PUBLIC_API_STABLE_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_B2BGEO_ROUTING_PUBLIC_API_STABLE_NETS_ ) |
| testing | [ \_B2BGEO_ROUTING_PUBLIC_API_TEST_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_B2BGEO_ROUTING_PUBLIC_API_TEST_NETS_ ) |

## [Lunapark load testing](https://lunapark.yandex-team.ru/firestarter/)
* Generate ammo via load_testing tool:
E.g. generate ammo for shooting at testing instance: `~/arcadia/maps/b2bgeo/tools/load_testing ya make -r; ./load_testing --url 'api-test.routing.yandex.net' -i scenarios/route.json -a f0b22049-31fa-4982-aad7-057c68ecf78b --rps 350 --duration 600 -s 1 -g`
* Choose instance for shooting and tank from one DC.
* Minimal config example: https://paste.yandex-team.ru/1135215

## API

All requests must contain `apikey` parameter.

### /v2/route

Build a route between known points.

| Method | GET |
| ------ | --- |
| **Params**   |
| waypoints | (required) Route points specified in decimal degrees (WGS84 standard).<br> Each point is defined as a coordinate pair in the format:<br> `{latitude},{longitude}`<br> Coordinate pairs (points) are separated by the pipe symbol (`|`). |
| mode | Routing mode. Possible values: `driving`, `walking`, `transit`, `truck`. |
| departure_time | The departure time in UNIX time. Used to calculate the expected traffic congestion. If this parameter is omitted, the traffic forecast is made for the time of sending the request.<br> This parameter is not used when calculating walking routes (`mode=walking`). |
| avoid_tolls | Avoid using toll roads. When `true`, the route goes around toll roads. Default value: `false`. |
| weight | Vehicle weight, tons. Used only with `mode=truck`. |
| axle_weight | Vehicle axle weight, tons. Used only with `mode=truck`. |
| max_weight | Maximum vehicle weight, tons. Used only with `mode=truck`. |
| height | Vehicle height, meters. Used only with `mode=truck`. |
| width | Vehicle width, meters. Used only with `mode=truck`. |
| length | Vehicle length, meters. Used only with `mode=truck`. |
| payload | Vehicle payload capacity, tons. Used only with `mode=truck`. |
| eco_class | Vehicle environmental class. Used only with `mode=truck`. |
| has_trailer | Vehicle has trailer flag. Used only with `mode=truck`. |

See also: [public documentation](https://yandex.ru/routing/doc/router/concepts/structure.html?lang=ru), [vehicle restrictions](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/veh.html)..

### /v2/distancematrix

Calculate the distance and duration of routes. Calculations are made for all possible combinations between the origin and destination.

| Method | GET |
| ------ | --- |
| **Params**   |
| origins | (required) Origin route points in decimal degrees (WGS84 standard).<br> Each point is defined as a coordinate pair in the format:<br> `{latitude},{longitude}`<br> Coordinate pairs (points) are separated by the pipe symbol (`|`). |
| destinations | (required) Destination route points in decimal degrees (WGS84 standard).<br> Each point is defined as a coordinate pair in the format:<br> `{latitude},{longitude}`<br> Coordinate pairs (points) are separated by the pipe symbol (`|`). |
| mode | Routing mode. Possible values: `driving`, `walking`, `transit`, `truck`. |
| router | Matrix router to use. Possible values: `main` (default), `global` (matrix router over osm), `alternative` (same as `global`). |
| departure_time | The departure time in UNIX time. Used to calculate the expected traffic congestion. If this parameter is omitted, the traffic forecast is made for the time of sending the request.<br> This parameter is not used when calculating walking routes (`mode=walking`). |
| weight | Vehicle weight, tons. Used only with `mode=truck`. |
| axle_weight | Vehicle axle weight, tons. Used only with `mode=truck`. |
| max_weight | Maximum vehicle weight, tons. Used only with `mode=truck`. |
| height | Vehicle height, meters. Used only with `mode=truck`. |
| width | Vehicle width, meters. Used only with `mode=truck`. |
| length | Vehicle length, meters. Used only with `mode=truck`. |
| payload | Vehicle payload capacity, tons. Used only with `mode=truck`. |
| eco_class | Vehicle environmental class. Used only with `mode=truck`. |
| has_trailer | Vehicle has trailer flag. Used only with `mode=truck`. |

See also: [public documentation](https://yandex.ru/routing/doc/distance_matrix/concepts/structure.html), [vehicle restrictions](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/veh.html).
