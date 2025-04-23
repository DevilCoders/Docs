# Core Inapp Backoffice

Backoffice-сервис приёма inapp-сообщений для последующей посылки.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Виктор Теплов (grok@yandex-team.ru) <br/> Владимир Фолунин (folunin@yandex-team.ru)|
| Отвественные SRE | Владимир Фолунин (folunin@yandex-team.ru) |
| Исходники | [maps/search/inapp/backoffice](https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/inapp/backoffice) |
| Сервис в ABC | [maps-core-inapp-backoffice](https://abc.yandex-team.ru/services/maps-core-inapp-backoffice/)|


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_inapp_backoffice_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_inapp_backoffice_stable/) | [ core-inapp-backoffice.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-inapp-backoffice-stable-panel-main/) | [ maps_core_inapp_backoffice_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_inapp_backoffice_stable) |
| Testing | [maps_core_inapp_backoffice_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_inapp_backoffice_testing/) | [ core-inapp-backoffice.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-inapp-backoffice-testing-panel-main/) | [ maps_core_inapp_backoffice_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_inapp_backoffice_testing) |


[Monitorings all (tag=a_prj_maps-core-inapp-backoffice)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-inapp-backoffice)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-inapp-backoffice.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-inapp-backoffice.maps.yandex.net/) | [core-inapp-backoffice.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-inapp-backoffice.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=core-inapp-backoffice-maps;signal=service_total) | [rtc_balancer_core-inapp-backoffice_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-inapp-backoffice_maps_yandex_net_man)<br>[rtc_balancer_core-inapp-backoffice_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-inapp-backoffice_maps_yandex_net_sas)<br>[rtc_balancer_core-inapp-backoffice_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-inapp-backoffice_maps_yandex_net_vla) |


## What happens when service is down

Невозможно послать новые inapp-сообщения.
На доставку сообщений посланных до отказа, не влияет.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/inapp-backoffice/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : use chyt.hahn; SELECT * FROM "//logs/maps-log/1d/2019-08-20" WHERE vhost LIKE 'core-inapp-backoffice.maps.yandex.net' LIMIT 1; |

## Documentation

https://wiki.yandex-team.ru/viktorteplov/drafts/inapp


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_INAPP_BACKOFFICE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_INAPP_BACKOFFICE_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_INAPP_BACKOFFICE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_INAPP_BACKOFFICE_TESTING_RTC_NETS_ ) |

