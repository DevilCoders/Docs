# indoor radiomap

Indoor радиокарта

## General information

- Кому звонить, если ничего не понятно: Алексей Пономарев ( ponomarev@yandex-team.ru ) Борис Чикунов ( chikunov@yandex-team.ru ) Илья Власюк ( tail@yandex-team.ru )
- [Исходники](https://a.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap)
- [Сервис в ABC](https://abc.yandex-team.ru/services/maps-core-indoor-radiomap)
- [CI (TestEnv) - Покоммитный](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_INDOOR_RADIOMAP)

## Instances

Сервисы в няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_indoor_radiomap/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_indoor_radiomap_stable/)
- [load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_indoor_radiomap_load/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_indoor_radiomap_testing/)

## Documentation

TODO

## Known clients

 - Mobile proxy

## Puncher

https://puncher.yandex-team.ru/?destination=core-indoor-radiomap.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination

_MAPS_CORE_MOBILE_PROXY_STABLE_RTC_NETS_ -> core-indoor-radiomap.maps.yandex.net

## Ecstatic Datasets
| Stable | Testing |
| ------ | ------- |
| [yandex-maps-indoor-radiomap](http://ecstatic.maps.yandex.net/pkg/yandex-maps-indoor-radiomap/versions) | [yandex-maps-indoor-radiomap](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-indoor-radiomap/versions) |
| [yandex-maps-indoor-radiomap-coverage](http://ecstatic.maps.yandex.net/pkg/yandex-maps-indoor-radiomap-coverage/versions) | [yandex-maps-indoor-radiomap-coverage](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-indoor-radiomap-coverage/versions) |


## What happens when service is down

TODO

## Как проверить, что сервис работает

Сделать запрос с какой-нибудь из машин `rtc:mobile_proxy_stable`
```
ssh <mobile-proxy-stable-host> curl -v http://core-indoor-radiomap.maps.yandex.net/ping 2>&1 |grep 200
```

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Балансеры

UI:
- [Production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-indoor-radiomap.maps.yandex.net/show/)
- [Testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-indoor-radiomap.testing.maps.yandex.net/show/)
- [Testing, service balancer](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-indoor-radiomap-testing-slb)

Balancers URL:
- Production: http://core-indoor-radiomap.maps.yandex.net
- Testing: http://core-indoor-radiomap.testing.maps.yandex.net
- Testing, service balancer: http://core-indoor-radiomap.testing.maps.n.yandex.ru

L3:
- [l3mgr stable](https://l3.tt.yandex-team.ru/service/7103)
- [l3mgr testing](https://l3.tt.yandex-team.ru/service/7102)

## Мониторинги

- [Juggler (Stable)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_indoor_radiomap_stable)
- [Juggler (Load)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_indoor_radiomap_load)
- [Juggler (Testing)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_indoor_radiomap_testing)

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-indoor-radiomap-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-indoor-radiomap-stable-panel-main) |
| Load | [maps-core-indoor-radiomap-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-indoor-radiomap-load-panel-main) |
| Testing | [maps-core-indoor-radiomap-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-indoor-radiomap-testing-panel-main) |

## SLA

TODO
[Statface](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_indoor_radiomap)

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| indoor-radiomap | `/var/log/yandex/maps/indoor-radiomap/*` |
| nginx | `/var/log/nginx/*` |
| yacare| `/var/log/yandex/maps/yacare/*` |
| supervisord | `/var/log/supervisor/*` |
| syslog (unfiltered) | `/var/log/syslog` |
| [YT](https://yql.yandex-team.ru/Operations/XVagkZ9Lnq4q-KtNYlq8OVIAD0-k7Qi9W68Amde_kZE=) | ``select * from hahn.`logs/maps-log/stream/5min/2019-08-15T18:00:00` where vhost like 'core-indoor-radiomap.maps.yandex.net'`` См. также в logs/maps-log/1d |

## Regression Stress Testing Configurations

- [Shootings](https://lunapark.yandex-team.ru/regress/NAVIGINE?service=indoor_radiomap)
- [Scheduler for imbalance shootings](https://sandbox.yandex-team.ru/scheduler/16936/view)
- [Scheduler for timing shootings](https://sandbox.yandex-team.ru/scheduler/16938/view)
