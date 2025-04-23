# Router proxy

Proxy from external clouds to core-maps routers.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | [abc:maps-b2bgeo-routerproxy](https://abc.yandex-team.ru/services/maps-b2bgeo-routerproxy/) |
| Отвественные SRE | Elena Markova (4c4d@yandex-team.ru) |
| Исходники | [maps/b2bgeo/router-proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/router-proxy) |
| Сервис в ABC | [maps-b2bgeo-routerproxy](https://abc.yandex-team.ru/services/maps-b2bgeo-routerproxy/)|
| CI - Покоммитный | https://a.yandex-team.ru/projects/maps-b2bgeo-routerproxy/ci/actions/launches?dir=maps%2Fb2bgeo%2Frouter-proxy&id=build |

## Service infrastructure

### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_b2bgeo_routerproxy_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routerproxy_prestable/) | [ b2bgeo-routerproxy.prestable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-routerproxy-prestable-panel-main/) | [ maps_b2bgeo_routerproxy_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_routerproxy_prestable) |
| Stable | [maps_b2bgeo_routerproxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routerproxy_stable/) | [ b2bgeo-routerproxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-routerproxy-stable-panel-main/) | [ maps_b2bgeo_routerproxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_routerproxy_stable) |
| Stress | [maps_b2bgeo_routerproxy_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routerproxy_stress/) | [ b2bgeo-routerproxy.stress ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-routerproxy-stress-panel-main/) | [ maps_b2bgeo_routerproxy_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_routerproxy_stress) |
| Testing | [maps_b2bgeo_routerproxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_routerproxy_testing/) | [ b2bgeo-routerproxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-routerproxy-testing-panel-main/) | [ maps_b2bgeo_routerproxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_routerproxy_testing) |

[Monitorings all (tag=a_prj_maps-b2bgeo-routerproxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-b2bgeo-routerproxy)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | default | [b2bgeo-routerproxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-routerproxy.maps.yandex.net/) | [b2bgeo-routerproxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas,man;fqdn=b2bgeo-routerproxy.maps.yandex.net;prj=b2bgeo-routerproxy-maps;signal=service_total;) | [rtc_balancer_b2bgeo-routerproxy_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-routerproxy_maps_yandex_net_man) <br>[rtc_balancer_b2bgeo-routerproxy_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-routerproxy_maps_yandex_net_sas) <br>[rtc_balancer_b2bgeo-routerproxy_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-routerproxy_maps_yandex_net_vla) |
| Testing | default | [b2bgeo-routerproxy.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-routerproxy.testing.maps.yandex.net/) | [b2bgeo-routerproxy.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas;fqdn=b2bgeo-routerproxy.testing.maps.yandex.net;prj=b2bgeo-routerproxy-testing-maps;signal=service_total;) | [rtc_balancer_b2bgeo-routerproxy_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-routerproxy_testing_maps_yandex_net_sas) <br>[rtc_balancer_b2bgeo-routerproxy_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-routerproxy_testing_maps_yandex_net_vla) |

### Firewall macroses

| staging | URL |
|---|---|
| Stable | [ \_MAPS_B2BGEO_ROUTERPROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_ROUTERPROXY_STABLE_RTC_NETS_ ) |
| Stress | [ \_MAPS_B2BGEO_ROUTERPROXY_STRESS_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_ROUTERPROXY_STRESS_RTC_NETS_ ) |
| Testing | [ \_MAPS_B2BGEO_ROUTERPROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_ROUTERPROXY_TESTING_RTC_NETS_ ) |


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/* |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Persistent Volumes

* /logs - логи, сюда ставится симлинка из /var/log
