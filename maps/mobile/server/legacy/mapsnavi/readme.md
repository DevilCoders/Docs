[TOC]
# Maps-Mobile-Legacy-MapsNavi

Provides road events (userpoi) to modern Yandex Navigator mobile application.

## Graphs
| Staging | URL |
|---|---|
| Prestable | https://yasm.yandex-team.ru/template/panel/maps-core-mobile-legacy-mapsnavi-prestable-panel-main/ |
| Stable | https://yasm.yandex-team.ru/template/panel/maps-core-mobile-legacy-mapsnavi-stable-panel-main/ |

## Monitoring
| Staging | URL |
|---|---|
| Prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dyasm.ambry.simple%26host%3Dmaps_core_mobile_legacy_mapsnavi_prestable|
| Stable | https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dyasm.ambry.simple%26host%3Dmaps_core_mobile_legacy_mapsnavi_stable|

## General information

| Topic | Information |
|---|---|
| Help | Алексей Хроленко (khrolenko@yandex-team.ru) Юрий Кирпичев (ykirpichev@yandex-team.ru) Вадим Мазаев (vmazaev@yandex-team.ru) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/legacy |
| ABC service | https://abc.yandex-team.ru/services/maps-core-mobile-legacy-mapsnavi |
| CI (TestEnv) | none |

## Instances

| Environment |  Nanny services |
|---|---|
| Prestable |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_legacy_mapsnavi_prestable/|
| Stable |https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_legacy_mapsnavi_stable/|

## Documentation

Mapsnavi service includes userpoi service.
All fastcgi services use localhost MYSQL instance in readonly mode 

## Ecstatic datasets

userpoi: yandex-maps-geobase-tzdata yandex-maps-geodata6

## What happens when the service is down

Legacy versions of maps and navi mobile applications loose part of it's functionality.

## How to fix common issues

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

At first figure out scope affected by the problem: service, host, sub-service.
If problem affects all hosts, it can be rtc problem, network problem or broken ecstatic dataset.
Check nginx logs on host.
Assure that all service are running.
Then check service logs in  /var/log/yandex/maps/mobile/
For more detailed logs edit service config in /etc/fastcgi2/available : set <level>INFO</level> to DEBUG and restart service via 'supervisorctl restart'

## Balancers
### Production:
- Porto metrics for the balancer container: https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-mobile-legacy-mapsnavi.maps.yandex.net;prj=maps-core-mobile-legacy-mapsnavi;ctype=prestable,stable;hosts=ASEARCH;itype=maps
- Generated Nanny services for the L7 balancers:
   - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-mobile-legacy-mapsnavi_maps_yandex_net_man/
   - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-mobile-legacy-mapsnavi_maps_yandex_net_sas/
   - https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-mobile-legacy-mapsnavi_maps_yandex_net_vla/
- Generated AWACS balancers:
   - https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-legacy-mapsnavi.maps.yandex.net
- Link to the farm in L3 manager:
   - mobile64.maps.yandex.net https://l3.tt.yandex-team.ru/service/2433
   - mobile-partners.maps.yandex.net https://l3.tt.yandex-team.ru/service/2456
- Firewall setup: `https://puncher.yandex-team.ru/?source=_MAPS_CORE_MOBILE_LEGACY_MAPSNAVI_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source`
- Firewall setup modifications through the puncher service: https://puncher.yandex-team.ru
- Balancers monitoring: https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-mobile-legacy-mapsnavi_maps_yandex_net_man%7Chost%3Drtc_balancer_core-mobile-legacy-mapsnavi_maps_yandex_net_sas%7Chost%3Drtc_balancer_core-mobile-legacy-mapsnavi_maps_yandex_net_vla&last=1DAY
### Balancers URLs:
- Production:
   - http://mobile64.maps.yandex.net
   - http://mobile-partners.maps.yandex.net
   - http://mobile.maps.yandex.net (alias to mobile64)
   - http://mobile.navi.yandex.net (alias to mobile64)

## SLA

- stats: https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_mobile_legacy_mapsnavi?scale=d&_period_distance=30&_incl_fields=d1&_incl_fields=d7&_incl_fields=d30&_incl_fields=n1&_incl_fields=n7&_incl_fields=n30
- config: https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_mobile_legacy_mapsnavi.py

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Userpoi | /var/log/yandex/maps/mobile/userpoi.* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.[logs/maps-log/1d/2019-08-21] WHERE vhost='mobile.maps.yandex.net' OR vhost='mobile-partners.maps.yandex.net' OR vhost='mobile64.maps.yandex.net' OR vhost='mobile.navi.yandex.net'; |


## Regression Stress Testing Configurations

none
