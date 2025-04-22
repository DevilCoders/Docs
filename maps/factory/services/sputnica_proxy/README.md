# Core Factory Sputnica Proxy

It's an external service that provides authorized access to some internal handles. It exchanges SessionId authorization cookie to TVM User-ticket and proxies requests to maps-core-factory-sputnica-back.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE | Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | [maps/factory/services/sputnica_proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/sputnica_proxy) |
| Сервис в ABC | [maps-core-factory-sputnica-proxy](https://abc.yandex-team.ru/services/maps-core-factory-sputnica-proxy/)|
| CI (TestEnv) - Покоммитный | [BUILD_DOCKER_MAPS_CORE_FACTORY_SPUTNICA_PROXY](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_FACTORY_SPUTNICA_PROXY) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_sputnica_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_sputnica_proxy_stable/) | [ core-factory-sputnica-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-sputnica-proxy-stable-panel-main/) | [ maps_core_factory_sputnica_proxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_sputnica_proxy_stable) |
| Testing | [maps_core_factory_sputnica_proxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_sputnica_proxy_testing/) | [ core-factory-sputnica-proxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-sputnica-proxy-testing-panel-main/) | [ maps_core_factory_sputnica_proxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_sputnica_proxy_testing) |


[Monitorings all (tag=a_prj_maps-core-factory-sputnica-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-sputnica-proxy)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-factory-sputnica-proxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-sputnica-proxy.maps.yandex.net/) | [core-factory-sputnica-proxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-sputnica-proxy.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man,vla;prj=core-factory-sputnica-proxy-maps;signal=service_total) | [rtc_balancer_core-factory-sputnica-proxy_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-sputnica-proxy_maps_yandex_net_man)<br>[rtc_balancer_core-factory-sputnica-proxy_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-sputnica-proxy_maps_yandex_net_sas)<br>[rtc_balancer_core-factory-sputnica-proxy_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-sputnica-proxy_maps_yandex_net_vla) |
| Testing | Default | [core-factory-sputnica-proxy.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-factory-sputnica-proxy.common.testing.maps.yandex.net_default/show/) |  |  |

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
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE ''<<yacare-service-name>>'.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)

## Known clients
Users of service spitnica.yandex.ru.


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FACTORY_SPUTNICA_PROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_SPUTNICA_PROXY_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FACTORY_SPUTNICA_PROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_SPUTNICA_PROXY_TESTING_RTC_NETS_ ) |
