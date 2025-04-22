# Core Core Nmaps Rdrproxy

Сервис предназначен для предоставления доступа некоторой группы внешних пользователей (картографы-аутсорсеры) к определенным внутренним ресурсам Яндекс.Карт, в частности к тайловому слою карт в [Картографе](https://cartograph.maps.yandex-team.ru/?service=mpro). Сервис использует ACL Народной Карты для контроля доступа к проксируемым слоям.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики |  quoter, ponomarev |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/rdrproxy |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-core-nmaps-rdrproxy/ |
| Проект в CI | [maps-core-nmaps-rdrproxy](https://a.yandex-team.ru/projects/maps-core-nmaps-rdrproxy/ci/actions/launches?dir=maps/wikimap/mapspro/services/rdrproxy) |


### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_rdrproxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_rdrproxy_stable/) | [ core-nmaps-rdrproxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-rdrproxy-stable-panel-main/) | [ maps_core_nmaps_rdrproxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_rdrproxy_stable) |
| Testing | [maps_core_nmaps_rdrproxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_rdrproxy_testing/) | [ core-nmaps-rdrproxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-rdrproxy-testing-panel-main/) | [ maps_core_nmaps_rdrproxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_rdrproxy_testing) |
[Monitorings all (tag=a_prj_maps-core-nmaps-rdrproxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-rdrproxy)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-nmaps-rdrproxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-rdrproxy.maps.yandex.net/) | [core-nmaps-rdrproxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-rdrproxy.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,man,sas;prj=core-nmaps-rdrproxy-maps;signal=service_total) | [rtc_balancer_core-nmaps-rdrproxy_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-rdrproxy_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-rdrproxy_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-rdrproxy_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-rdrproxy_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-rdrproxy_maps_yandex_net_vla) |
| Testing | Default | [core-nmaps-rdrproxy.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-rdrproxy.testing.maps.yandex.net/) | [core-nmaps-rdrproxy.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-rdrproxy.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-nmaps-rdrproxy-testing-maps;signal=service_total) | [rtc_balancer_core-nmaps-rdrproxy_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-rdrproxy_testing_maps_yandex_net_sas) |

## What happens when service is down

У пользователей не отображаются подключенные вспомогательные растровые слои.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/wiki-rdr-proxy/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : USE hahn; SELECT * FROM [logs/maps-log/1d/2018-09-20] WHERE tskv_format='wiki-rdr-proxy'; |

## How to fix common problems
Сервис занимается проверкой прав доступа и проксированием запросов к внутренним сервисам. 
Проблема может возникнуть либо на этапе проверке прав доступа, либо на этапе выполнения запроса к внутреннему сервису. 
Чтобы определить причину, нужно посмотреть логи `/var/log/yandex/maps/wiki-rdr-proxy/wiki-rdr-proxy.log`. 

Ошибки обращения к внутренним сервисам в логах будут выглядеть примерно так:
```
GET /layer/cartograph?revision=9046&x=95781&y=41733&z=17 => HTTP 500: cannot connect to core-renderer-cartograph.maps.yandex.net: Operation now in progress
```
В этом случае, нужно связаться с ответственными разработчиками соответствующего сервиса:
- для слоя `cartograph`: [maps-core-renderer-cartograph](https://abc.yandex-team.ru/services/maps-core-renderer-cartograph)
- для слоя `satellite`: [maps-core-factory-renderer](https://abc.yandex-team.ru/services/maps-core-factory-renderer)

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/rdrproxy/

## Known clients
- Пользователи Народной Карты


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_RDRPROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_RDRPROXY_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_RDRPROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_RDRPROXY_TESTING_RTC_NETS_ ) |

