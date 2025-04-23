# Core Masstransit Partners Proxy

Сервис устанавливает OpenVPN соединение с поставщиком данных (ЦОДД) и проксирует HTTP запросы на внутренние сервера этого поставщика.

На стороне поставщика есть "идеологическое" ограничение, позволяющее открывать VPN соединение с одним сертификатом только с одного IP адреса.
В силу того, что у нас есть только 2 сертификата, для отказоустойчивости прокси приходится ограничиваться только stable окружением
с одной машинкой в каждом из двух ДЦ. Сервисы-клиенты из всех окружений ходят в stable окружение данной прокси.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [Антон Овчинкин](https://staff.yandex-team.ru/ovchinkin), [Андрей Козлов](https://staff.yandex-team.ru/pedeathtrian) |
| Исходники | [maps/masstransit/info/partners_proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/partners_proxy) |
| Сервис в ABC | [maps-core-masstransit-partners-proxy](https://abc.yandex-team.ru/services/maps-core-masstransit-partners-proxy/)|
| Проект в CI | [maps-core-masstransit-partners-proxy](https://a.yandex-team.ru/projects/maps-core-masstransit-partners-proxy/ci/actions/launches?dir=maps/masstransit/info/partners_proxy)|


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_masstransit_partners_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_masstransit_partners_proxy_stable/) | [ core-masstransit-partners-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-partners-proxy-stable-panel-main/) | [ maps_core_masstransit_partners_proxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_masstransit_partners_proxy_stable) |

[Monitorings all (tag=a_prj_maps-core-masstransit-partners-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-masstransit-partners-proxy)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-masstransit-partners-proxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-masstransit-partners-proxy.maps.yandex.net/) | [core-masstransit-partners-proxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-masstransit-partners-proxy.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas;prj=core-masstransit-partners-proxy-maps;signal=service_total) | [rtc_balancer_core-masstransit-partners-proxy_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-partners-proxy_maps_yandex_net_sas)<br>[rtc_balancer_core-masstransit-partners-proxy_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-masstransit-partners-proxy_maps_yandex_net_vla) |


## What happens when service is down

Перестают отображаться метки и прогнозы прибытия транспорта в Москве.

## Logs
| Name | URL/path |
|---|---|
| Nginx | `/var/log/nginx/*` |
| Supervisord | `/var/log/supervisor/*` |
| Openvpn | `/var/log/supervisor/openvpn-stdout*` |
| Syslog (unfiltered) | `/var/log/syslog` |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Если все запросы завершаются с ошибкой или таймаутятся, можно попробовать порестартить openvpn:
`supervisorctl restart openvpn`

## Known clients
- [maps_core_masstransit_realtime_receiving](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/realtime_receiving/)


## Persistent Volumes
* `/logs` - логи, сюда ставится симлинка из `/var/log`

## Firewall macros
| staging | URL |
|---|---|
| stable | [ `_MAPS_CORE_MASSTRANSIT_PARTNERS_PROXY_STABLE_RTC_NETS_` ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MASSTRANSIT_PARTNERS_PROXY_STABLE_RTC_NETS_ ) |
