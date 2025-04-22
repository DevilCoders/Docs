# Core Startrek Proxy

A service for creating MAPKITSIM tasks and uploading user tracks to YT

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Александр Любицкий (innocent@yandex-team.ru) Пётр Гриневич (grinev@yandex-team.ru)|
| Отвественные SRE | Александр Любицкий (innocent@yandex-team.ru) Пётр Гриневич (grinev@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/startrek-proxy |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-startrek-proxy/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_MAPS_CORE_STARTREK_PROXY_DOCKER |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_startrek_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_startrek_proxy_stable/) | [ core-startrek-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-startrek-proxy-stable-panel-main/) | [ maps_core_startrek_proxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_startrek_proxy_stable) |
| Testing | [maps_core_startrek_proxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_startrek_proxy_testing/) | [ core-startrek-proxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-startrek-proxy-testing-panel-main/) | [ maps_core_startrek_proxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_startrek_proxy_testing) |
[Monitorings all (tag=a_prj_maps-core-startrek-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-startrek-proxy)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-startrek-proxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-startrek-proxy.maps.yandex.net/) | [core-startrek-proxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-startrek-proxy.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,msk;prj=core-startrek-proxy-maps;signal=service_total) | [rtc_balancer_core-startrek-proxy_maps_yandex_net_iva](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-startrek-proxy_maps_yandex_net_iva)<br>[rtc_balancer_core-startrek-proxy_maps_yandex_net_myt](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-startrek-proxy_maps_yandex_net_myt)<br>[rtc_balancer_core-startrek-proxy_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-startrek-proxy_maps_yandex_net_sas) |
| Testing | Default | [core-startrek-proxy.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-startrek-proxy.testing.maps.yandex.net/) | [core-startrek-proxy.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-startrek-proxy.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-startrek-proxy-testing-maps;signal=service_total) | [rtc_balancer_core-startrek-proxy_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-startrek-proxy_testing_maps_yandex_net_sas) |
## What happens when service is down

MAPKITSIM tasks are no longer created and tracks are not uploaded to YT

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/stproxy/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2019-11-05\` WHERE vhost LIKE 'core-startrek-proxy.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Known clients
- maps_core_mobile_proxy

## SLA
Сервис внутренний, SLA не нужны

## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macros
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_STARTREK_PROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STARTREK_PROXY_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_STARTREK_PROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STARTREK_PROXY_TESTING_RTC_NETS_ ) |

## TVM authorization
Startrek-proxy использует TVM-авторизацию для запросов в Черный ящик
ID TVM-приложений можно посмотреть в [ABC](https://abc.yandex-team.ru/services/maps-core-push-proxy/resources/)

## BlackBox access & grants
Startrek-proxy получает из Черного Ящика информацию, имеет ли пользователь привязанный внутренний логин @yandex-team.ru (то есть является сотрудником Яндекса)
Для этого получены следующие гранты:
[testing](https://st.yandex-team.ru/PASSPORTGRANTS-2740)
[stable](https://st.yandex-team.ru/PASSPORTGRANTS-2741)
