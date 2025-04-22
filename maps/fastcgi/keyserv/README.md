# keyserv

Keyserv - управление пользователями API Карт

## General information

- Кому звонить, если ничего не понятно: Борис Чикунов ( chikunov@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) Евклид Никифоров ( euclid@yandex-team.ru )
- [Исходники](https://a.yandex-team.ru/arc/trunk/arcadia/maps/fastcgi/keyserv)
- [Сервис в ABC](https://abc.yandex-team.ru/services/maps-core-keyserv/)
- [CI (TestEnv) - Покоммитный](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_KEYSERV)

## Instances

Сервисы в няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_keyserv/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_keyserv_stable/)
- [prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_keyserv_prestable/)
- [load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_keyserv_load/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_keyserv_testing/)

## Documentation

[Wiki](https://wiki.yandex-team.ru/maps/dev/core/keyserv2/)

## Known clients

 - JS API
 - JS API сервисы
 - Static API
 - apikeys-int
 - http геокодер
 - LBS

## Puncher

https://puncher.yandex-team.ru/?destination=core-keyserv.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination

keyserv -> `_PGAASINTERNALNETS_:6432`

`_SEARCHPRODNETS_`,`_MAPSPRODQNETS_`,`_MAPSNETS_`,`_TECH_PROD_SRV_` -> core-keyserv.maps.yandex.net

## ecstatic Datasets

Нет

## MDB Postgresql clusters

- [Stable](https://yc.yandex-team.ru/folders/foo33ascbp6eve169b8e/managed-postgresql/cluster/mdbt3lq4ipftb3eeoecs)
- [Testing](https://yc.yandex-team.ru/folders/foo33ascbp6eve169b8e/managed-postgresql/cluster/mdbg8j91lp7h4c8f2qau)
- [Load](https://yc.yandex-team.ru/folders/foo33ascbp6eve169b8e/managed-postgresql/cluster/mdbkqvspaiv48ne74mhc)

## What happens when service is down

Клиенты (сервисы, предоставялющие API) работают в режиме "всем разрешено всё". Данная логика обеспечивается на стороне сервисов.

## Как проверить, что сервис работает

Сделать запрос с какой-нибудь из машин `%maps_api`
```
executer> exec %maps_api curl -v http://core-keyserv.maps.yandex.net/ping 2>&1 |grep 200
```

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

UI:
- [Production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-keyserv.maps.yandex.net/show/)
- [Testing](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-keyserv-testing-slb)

Balancers URL:
- Production: http://core-keyserv.maps.yandex.net
- Testing: http://core-keyserv.testing.maps.n.yandex.ru

[l3mgr](https://l3.tt.yandex-team.ru/service/5474)

## Мониторинги

- [Juggler (Stable)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_keyserv_stable)
- [Juggler (Prestable)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_keyserv_prestable)
- [Juggler (Load)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_keyserv_load)
- [Juggler (Testing)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_keyserv_testing)

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable + Prestable | [maps-core-keyserv-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-keyserv-stable-panel-main) |
| Prestable | [maps-core-keyserv-prestable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-keyserv-prestable-panel-main) |
| Load | [maps-core-keyserv-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-keyserv-load-panel-main) |
| Testing | [maps-core-keyserv-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-keyserv-testing-panel-main) |
| DB Stable | [https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbt3lq4ipftb3eeoecs;dbname=mapapikeys/](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbt3lq4ipftb3eeoecs;dbname=mapapikeys/) |
| DB Load | [https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbkqvspaiv48ne74mhc;dbname=mapapikeys/](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbkqvspaiv48ne74mhc;dbname=mapapikeys/) |
| DB Testing | [https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg8j91lp7h4c8f2qau;dbname=mapapikeys/](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbg8j91lp7h4c8f2qau;dbname=mapapikeys/) |

## SLA

[Statface](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_keyserv)

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| keyserv | `/var/log/yandex/maps/keyserv/*` |
| nginx | `/var/log/nginx/*` |
| yacare| `/var/log/yandex/maps/yacare/*` |
| supervisord | `/var/log/supervisor/*` |
| syslog (unfiltered) | `/var/log/syslog` |
| [YT](https://yql.yandex-team.ru/Operations/XU1pcza9vMzKWtWi3JGdt3Ei-LJ5NrxvIBNm24SEIps=) | ``select * from hahn.`logs/maps-log/stream/5min/2019-08-08T18:45:00` where vhost like 'core-keyserv.maps.yandex.net'`` См. также в logs/maps-log/1d |

## Regression Stress Testing Configurations

- [Shootings](https://lunapark.yandex-team.ru/regress/MAPSCORE?service=Keyserv)
- [Scheduler for imbalance shootings](https://sandbox.yandex-team.ru/scheduler/13921/view)
- [Scheduler for timing shootings](https://sandbox.yandex-team.ru/scheduler/13922/view)
