# Ratelimiter 

Ограничитель частоты запросов для распределенных сервисов.
Позволяет определить баланс нагрузки между клиентами и задать квоты.

При подключении, на машины сервиса устанавлиается агент рейтлимитера, интегрированный c nginx.
Агенты связываются с сервером рейтлимитера для поддержания синхронного состояния счетчиков запросов.

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Лёша Савин([alexey-savin@](https://staff.yandex-team.ru/alexey-savin)), Юра Кирпичёв([ykirpichev@](https://staff.yandex-team.ru/ykirpichev)), Андрей Андреев([comradeandrew@](https://staff.yandex-team.ru/comradeandrew)) |
| SRE |  |
| Сервис в ABC | [maps-core-ratelimiter](https://abc.yandex-team.ru/services/maps-core-ratelimiter) |
| Конфигурация лимитов | [maps/config/ratelimiter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter) |
| Исходники | [maps/infra/ratelimiter2](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2) |
| Исходники sandbox-задач| [sandbox/projects/maps/RateLimitsRefresher](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/RateLimitsRefresher) |
| CI (TestEnv) покоммитная сборка| [BUILD_DOCKER_MAPS_CORE_RATELIMITER](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_RATELIMITER) |
| CI (TestEnv) покоммитное обновление лимитов| [RATELIMITER_UPLOAD_CONFIGS_STABLE](https://testenv.yandex-team.ru/?screen=job_history&database=maps_geoinfra_tests&job_name=RATELIMITER_UPLOAD_CONFIGS_STABLE) <br> [RATELIMITER_UPLOAD_CONFIGS_LOAD](https://testenv.yandex-team.ru/?screen=job_history&database=maps_geoinfra_tests&job_name=RATELIMITER_UPLOAD_CONFIGS_LOAD) <br> [RATELIMITER_UPLOAD_CONFIGS_TESTING](https://testenv.yandex-team.ru/?screen=job_history&database=maps_geoinfra_tests&job_name=RATELIMITER_UPLOAD_CONFIGS_TESTING) |
| Tracker Queue | https://st.yandex-team.ru/GEOINFRA |

## Instances

| Environment | URL |
|---|---|
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ratelimiter_stable/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ratelimiter_prestable/ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ratelimiter_load/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ratelimiter_testing/ |

| Dashboard |
|---|
| https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_ratelimiter |

## Documentation

https://wiki.yandex-team.ru/geo-infra/ratelimiter2-manual

Design review: https://wiki.yandex-team.ru/users/kibergus/ratelimiter2.0/


## Known clients

Мобильная прокси [maps/mobile/proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/proxy). Графики нагрузки: [клик](https://yasm.yandex-team.ru/template/panel/maps_mobile-ratelimiter2-panel/?range=86400000)

Driving router [maps/routing/router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router), Графики нагрузки: [клик](https://yasm.yandex-team.ru/template/panel/maps_core_driving_router-ratelimiter2-panel/?range=86400000)

Дорожные события [wiki/maps_info](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_info), Графики нагрузки: [клик](https://yasm.yandex-team.ru/template/panel/infopoint-ratelimiter2-panel/?range=86400000)

## What happens when service is down

Перестанут соблюдаться квоты на количество запросов, т.к. не будет синхронизации счетчиков между агентами на разных машинах.

Агенты не будут получать обновления конфигурации лимитов.


## How to fix common problems

Аварийный способ быстро отключить агент рейтлимитера на отдельной машине (нужно sudo):
```
bash /usr/lib/yandex/maps/ratelimiter2/agent-ctl.sh disable
```
Например если рейтлимитер взбесится и начнет банить все запросы подряд.
Когда причины устранены то, чтобы включить агента:
```
bash /usr/lib/yandex/maps/ratelimiter2/agent-ctl.sh enable
```

## Monitorings

| Staging | Juggler panel |
|---|---|
| Stable | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_ratelimiter_stable |
| Prestable | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_ratelimiter_prestable |
| Load | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_ratelimiter_load |
| Testing | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_ratelimiter_testing |


## Graphics

| Staging | Golovan panel |
|---|---|
| Stable | https://yasm.yandex-team.ru/template/panel/maps-core-ratelimiter-stable-panel-main |
| Prestable | https://yasm.yandex-team.ru/template/panel/maps-core-ratelimiter-prestable-panel-main |
| Load | https://yasm.yandex-team.ru/template/panel/maps-core-ratelimiter-load-panel-main |
| Testing | https://yasm.yandex-team.ru/template/panel/maps-core-ratelimiter-testing-panel-main |


## Logs

Логи сервера искать в контейнерах в Няне.

| | |
|---|---|
| Ratelimiter server | /var/log/yandex/maps/ratelimiter-server/* |
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/* |
| YT | https://yql.yandex-team.ru SELECT * FROM hahn.[logs/maps-log/1d/2019-08-08] WHERE vhost LIKE 'core-ratelimiter.maps.yandex.net' (логи всех stable и prestable инстансов)

Логи агентов на машинах подключенных сервисов

| | |
|---|---|
| Ratelimiter proxy | /var/log/yandex/maps/ratelimiter-proxy/* |
| Nginx | /var/log/nginx/* |

## Balancers
Агенты используют адрес балансера при получении и обновлении списка инстансов сервера (периодические запросы на ручку /upstream/instances).
Для синхронизации счетчиков агенты обращаются напрямую к инстансам.

Также балансер использует sandbox таск для загрузки обновления конфигурации лимитов на сервер.

#### Production - core-ratelimiter.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/4251
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=5807
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ratelimiter.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/ckaDLLbmk/l3-vs-core-ratelimiter-maps-yandex-net
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ratelimiter.maps.yandex.net/show/
  * Графики
    * Common metrics: https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-ratelimiter.maps.yandex.net;prj=core-ratelimiter-maps;ctype=prod;timelines=0.2,0.4,0.7,1,2,10/
    * Portoinst metrics: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-ratelimiter.maps.yandex.net;prj=core-ratelimiter-maps;ctype=prod/
  * Мониторинги: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-ratelimiter_maps_yandex_net_man%7Chost%3Drtc_balancer_core-ratelimiter_maps_yandex_net_vla%7Chost%3Drtc_balancer_core-ratelimiter_maps_yandex_net_sas&statuses=WARN%2CCRIT%2COK
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-ratelimiter.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination

#### Testing - core-ratelimiter.testing.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/4243
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=5801
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ratelimiter.testing.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/9ZpLVJxmk/l3-vs-core-ratelimiter-testing-maps-yandex-net
* L7
  * AWACS: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ratelimiter.testing.maps.yandex.net/show/
  * Графики
    * Common metrics: https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-ratelimiter.testing.maps.yandex.net;prj=core-ratelimiter-testing-maps;ctype=prod;timelines=0.2,0.4,0.7,1,2,10/
    * Portoinst metrics: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-ratelimiter.testing.maps.yandex.net;prj=core-ratelimiter-testing-maps;ctype=prod/
  * Мониторинги: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-ratelimiter_testing_maps_yandex_net_man%7Chost%3Drtc_balancer_core-ratelimiter_testing_maps_yandex_net_vla%7Chost%3Drtc_balancer_core-ratelimiter_testing_maps_yandex_net_sas&statuses=WARN%2CCRIT%2COK
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-ratelimiter.testing.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination


## MDB resources

Для каждого стейджинга, во внутреннем облаке заведен mongodb кластер с replica set из 3х инстансов размера 'db1.nano' (по одному в man, vla и sas датацентрах).  
Дашборды: [Stable](https://yc.yandex-team.ru/folders/foodbrg01p0tcr87v4l5/managed-mongodb/cluster/146d3acc-7ca2-4321-9f10-e8657240dd86),
[Testing](https://yc.yandex-team.ru/folders/foodbrg01p0tcr87v4l5/managed-mongodb/cluster/01da18e8-0869-408e-a649-81d15037b6af),
[Load](https://yc.yandex-team.ru/folders/foodbrg01p0tcr87v4l5/managed-mongodb/cluster/98b9062d-01fa-4250-ab59-a5e67a1edb9b)


Графики в Головане: [Stable](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=146d3acc-7ca2-4321-9f10-e8657240dd86),
[Testing](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=01da18e8-0869-408e-a649-81d15037b6af),
[Load](https://yasm.yandex-team.ru/template/panel/dbaas_mongodb_metrics/cid=98b9062d-01fa-4250-ab59-a5e67a1edb9b)


Также для управления, можно использовать Yandex.Cloud CLI:
```
yc managed-mongodb --folder-name maps-core-ratelimiter cluster get --name maps_core_ratelimiter_testing
```
## SLA

99.9% запросов к серверу обрабытываются корректно, меньше чем за 100ms
[Статистика](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_ratelimiter)

## Regression Stress Testing

| Type | URL |
|---|---|
| Графики | https://lunapark.yandex-team.ru/regress/GEOINFRA?service=maps-core-ratelimiter |
| CI (Sandbox) | https://sandbox.yandex-team.ru/scheduler/10615/view |
| Тикет | https://st.yandex-team.ru/GEOINFRA-410  | 
| Исходники sandbox-задач|[sandbox/projects/maps/MapsRatelimiter2Shooter](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsRatelimiter2Shooter) <br> [sandbox/projects/maps/MapsRatelimiter2AmmoGen](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsRatelimiter2AmmoGen)|

