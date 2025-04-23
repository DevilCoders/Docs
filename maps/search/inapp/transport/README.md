# Core Inapp Transport

Сервис доставки inapp-сообщений.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Виктор Теплов (grok@yandex-team.ru) <br/> Пётр Лежанкин (lepetrandr@yandex-team.ru) |
| Отвественные SRE | Пётр Лежанкин (lepetrandr@yandex-team.ru)  |
| Исходники | [maps/search/inapp/transport](https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/inapp/transport) |
| Сервис в ABC | [maps-core-inapp-transport](https://abc.yandex-team.ru/services/maps-core-inapp-transport/)|


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_core_inapp_transport_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_inapp_transport_prestable/) | [ core-inapp-transport.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-inapp-transport-prestable-panel-main/) | [ maps_core_inapp_transport_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_inapp_transport_prestable) |
| Stable | [maps_core_inapp_transport_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_inapp_transport_stable/) | [ core-inapp-transport.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-inapp-transport-stable-panel-main/) | [ maps_core_inapp_transport_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_inapp_transport_stable) |
| Testing | [maps_core_inapp_transport_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_inapp_transport_testing/) | [ core-inapp-transport.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-inapp-transport-testing-panel-main/) | [ maps_core_inapp_transport_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_inapp_transport_testing) |


[Monitorings all (tag=a_prj_maps-core-inapp-transport)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-inapp-transport)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-inapp-transport.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-inapp-transport.maps.yandex.net/) | [core-inapp-transport.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-inapp-transport.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man,vla;prj=core-inapp-transport-maps;signal=service_total) | [rtc_balancer_core-inapp-transport_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-inapp-transport_maps_yandex_net_man)<br>[rtc_balancer_core-inapp-transport_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-inapp-transport_maps_yandex_net_sas)<br>[rtc_balancer_core-inapp-transport_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-inapp-transport_maps_yandex_net_vla) |


## What happens when service is down

Inapp-сообщения не доставляются клиентам.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/inapp-transport/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : use chyt.hahn; SELECT * FROM "//logs/maps-log/1d/2019-08-20" WHERE vhost LIKE 'core-inapp-transport.maps.yandex.net' LIMIT 1; |


## Documentation

https://wiki.yandex-team.ru/viktorteplov/drafts/inapp


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_INAPP_TRANSPORT_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_INAPP_TRANSPORT_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_INAPP_TRANSPORT_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_INAPP_TRANSPORT_TESTING_RTC_NETS_ ) |

