# wiki-acl

ACL Народной карты

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Евклид Никифоров ( euclid@yandex-team.ru ) Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/acl |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-acl/ |
| Проект в CI | [maps-core-nmaps-acl](https://a.yandex-team.ru/projects/maps-core-nmaps-acl/ci/actions/launches?dir=maps/wikimap/mapspro/services/acl) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_acl/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_acl_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_acl_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_acl_unstable/)
- [load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_acl_load/)

## Documentation

Схема: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/schemas/acl

## Known clients

https://puncher.yandex-team.ru/?destination=core-nmaps-acl.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination

wiki-acl -> `_PGAASINTERNALNETS_`:6432

`_MAPSPRODQNETS_`,`_MAPSNETS_` -> wiki-acl:80

## ecstatic Datasets

Нет

## What happens when service is down

Единая и Народная карты не будут работать

## Как проверить, что сервис работает

Сделать запрос с какой-нибудь из машин %maps_um_back
executer> exec %maps_um_back curl -v http://core-nmaps-acl.maps.yandex.net/ping 2>&1 |grep 200

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | default | [core-nmaps-acl.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-acl.maps.yandex.net/) | [core-nmaps-acl.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla;fqdn=core-nmaps-acl.maps.yandex.net;prj=core-nmaps-acl-maps;signal=service_total;) | [rtc_balancer_core-nmaps-acl_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-acl_maps_yandex_net_sas) <br>[rtc_balancer_core-nmaps-acl_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-acl_maps_yandex_net_vla) |
| Testing | common_default | [core-nmaps-acl.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-acl.common.testing.maps.yandex.net"}) | [core-nmaps-acl.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-nmaps-acl_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |
| Unstable | common_default | [core-nmaps-acl.common.unstable.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.unstable.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-acl.common.unstable.maps.yandex.net"}) | [core-nmaps-acl.common.unstable.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.unstable.maps.yandex.net;prj=common.unstable.maps.yandex.net;signal=core-nmaps-acl_common_unstable_maps_yandex_net;) | [rtc_balancer_common_unstable_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_sas) <br>[rtc_balancer_common_unstable_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_man) <br>[rtc_balancer_common_unstable_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_vla) |

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_acl_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_acl_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_acl_unstable |
| Juggler (Load) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_acl_load |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-acl-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-acl-stable-panel-main) |
| Testing | [maps-core-nmaps-acl-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-acl-testing-panel-main) |
| Unstable | [maps-core-nmaps-acl-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-acl-unstable-panel-main) |
| Load | [maps-core-nmaps-acl-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-acl-load-panel-main) |
| database | [mapspro_core](https://yasm.yandex-team.ru/panel/chikunov.mapspro_core/) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| wiki-acl | /var/log/yandex/maps/wiki-acl/* |
| nginx | /var/log/nginx/* |
| yacare| /var/log/yandex/maps/yacare/* |
| supervisord | /var/log/supervisor/* |
| syslog (unfiltered) | /var/log/syslog |

## Regression Stress Testing Configurations

- [Shootings](https://lunapark.yandex-team.ru/regress/NMAPS?service=ACL)
- [Scheduler for imbalance shootings](https://sandbox.yandex-team.ru/scheduler/13977/view)
- [Scheduler for timing shootings](https://sandbox.yandex-team.ru/scheduler/13978/view)

## Патч в DNS для UI
core-nmaps-acl.load.maps.yandex.net is an alias for **YP-POD from maps_core_nmaps_acl_load**

Можно получить динамически из [API Няни](https://nanny.yandex-team.ru/v2/services/maps_core_nmaps_acl_load/current_state/instances/)
