# Core Sprav Callcenter Api

Коллцентр

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Анна Ждан (likynushka@yandex-team.ru) Алексей Градсков (gradksov@yandex-team.ru) Андрей Дроздовский (tagrimar@yandex-team.ru) |
| Отвественные SRE |  |
| Исходники | [maps/sprav/callcenter/api](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/callcenter/api) |
| Сервис в ABC | [maps-core-sprav-callcenter-api](https://abc.yandex-team.ru/services/maps-core-sprav-callcenter-api/)|
| Проект в CI | [maps-core-sprav-callcenter-api](https://a.yandex-team.ru/projects/maps-core-sprav-callcenter-api/ci/actions/launches?dir=maps/sprav/callcenter/api) |

## Service infrastructure

### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_core_sprav_callcenter_api_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sprav_callcenter_api_prestable/) | [ core-sprav-callcenter-api.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-sprav-callcenter-api-prestable-panel-main/) | [ maps_core_sprav_callcenter_api_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sprav_callcenter_api_prestable) |
| Stable | [maps_core_sprav_callcenter_api_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sprav_callcenter_api_stable/) | [ core-sprav-callcenter-api.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-sprav-callcenter-api-stable-panel-main/) | [ maps_core_sprav_callcenter_api_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sprav_callcenter_api_stable) |
| Testing | [maps_core_sprav_callcenter_api_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sprav_callcenter_api_testing/) | [ core-sprav-callcenter-api.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-sprav-callcenter-api-testing-panel-main/) | [ maps_core_sprav_callcenter_api_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sprav_callcenter_api_testing) |

[Monitorings all (tag=a_prj_maps-core-sprav-callcenter-api)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-sprav-callcenter-api)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | default | [core-sprav-callcenter-api.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-sprav-callcenter-api.maps.yandex.net/) | [core-sprav-callcenter-api.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=man,sas,vla;fqdn=core-sprav-callcenter-api.maps.yandex.net;prj=core-sprav-callcenter-api-maps;signal=service_total;) | [rtc_balancer_core-sprav-callcenter-api_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sprav-callcenter-api_maps_yandex_net_man) <br>[rtc_balancer_core-sprav-callcenter-api_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sprav-callcenter-api_maps_yandex_net_sas) <br>[rtc_balancer_core-sprav-callcenter-api_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sprav-callcenter-api_maps_yandex_net_vla) |
| Testing | default | [core-sprav-callcenter-api.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-sprav-callcenter-api.testing.maps.yandex.net/) | [core-sprav-callcenter-api.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla;fqdn=core-sprav-callcenter-api.testing.maps.yandex.net;prj=core-sprav-callcenter-api-testing-maps;signal=service_total;) | [rtc_balancer_core-sprav-callcenter-api_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sprav-callcenter-api_testing_maps_yandex_net_sas) <br>[rtc_balancer_core-sprav-callcenter-api_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sprav-callcenter-api_testing_maps_yandex_net_vla) |

### Firewall macroses

| staging | URL |
|---|---|
| Stable | [ \_MAPS_CORE_SPRAV_CALLCENTER_API_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SPRAV_CALLCENTER_API_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_CORE_SPRAV_CALLCENTER_API_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SPRAV_CALLCENTER_API_TESTING_RTC_NETS_ ) |

## What happens when service is down

TODO: Напишите, что происходит при отказе сервиса

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2022-02-20` WHERE vhost LIKE ''core-sprav-callcenter-api'.maps.yandex.net' limit 1; |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

* <https://docs.yandex-team.ru/sprav/callcenter/intro>
* CI: <https://a.yandex-team.ru/projects/maps-core-sprav-callcenter-api/ci>

## Known clients

TODO: Сюда напишите список известных клиентов

## Persistent Volumes

* /logs - логи, сюда ставится симлинка из /var/log
