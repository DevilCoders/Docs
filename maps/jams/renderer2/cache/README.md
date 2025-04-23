# Core Jams Rdr Cache

Кэширующий сервис для тайлов пробок и дорожных событий (trf, trfe, trj, trje). Представляет собой nginx с кэшом, проксирующий запросы в рендерер пробок [core-jams-rdr.maps.yandex.net](https://abc.yandex-team.ru/services/maps-core-jams-rdr/).

Для увеличения cache hit'а на production балансерах используется хэширование. Расчетный cache hit - 50%.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Александр Любицкий (innocent@yandex-team.ru) <br> Евгения Мордашова (morevi@yandex-team.ru) |
| Исходники | [maps/jams/renderer2/cache](https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/renderer2/cache) |
| Сервис в ABC | [maps-core-jams-rdr-cache](https://abc.yandex-team.ru/services/maps-core-jams-rdr-cache/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_JAMS_RDR_CACHE |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Load | [maps_core_jams_rdr_cache_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_cache_load/) | [ core-jams-rdr-cache.load ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-cache-load-panel-main/) | [ maps_core_jams_rdr_cache_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_cache_load) |
| Prestable | [maps_core_jams_rdr_cache_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_cache_prestable/) | [ core-jams-rdr-cache.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-cache-prestable-panel-main/) | [ maps_core_jams_rdr_cache_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_cache_prestable) |
| Stable | [maps_core_jams_rdr_cache_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_cache_stable/) | [ core-jams-rdr-cache.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-cache-stable-panel-main/) | [ maps_core_jams_rdr_cache_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_cache_stable) |
| Testing | [maps_core_jams_rdr_cache_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_cache_testing/) | [ core-jams-rdr-cache.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-cache-testing-panel-main/) | [ maps_core_jams_rdr_cache_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_cache_testing) |


[Monitorings all (tag=a_prj_maps-core-jams-rdr-cache)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-jams-rdr-cache)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-jams-rdr-cache.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-rdr-cache.maps.yandex.net/) | [core-jams-rdr-cache.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-rdr-cache.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-jams-rdr-cache-maps;signal=service_total) | [rtc_balancer_core-jams-rdr-cache_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache_maps_yandex_net_man)<br>[rtc_balancer_core-jams-rdr-cache_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache_maps_yandex_net_sas)<br>[rtc_balancer_core-jams-rdr-cache_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache_maps_yandex_net_vla) |
| Stable | Internal | [core-jams-rdr-cache-internal.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-rdr-cache-internal.maps.yandex.net/) | [core-jams-rdr-cache-internal.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-rdr-cache-internal.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-jams-rdr-cache-internal-stable-balancer;signal=service_total) | [rtc_balancer_core-jams-rdr-cache-internal_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache-internal_maps_yandex_net_man)<br>[rtc_balancer_core-jams-rdr-cache-internal_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache-internal_maps_yandex_net_sas)<br>[rtc_balancer_core-jams-rdr-cache-internal_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache-internal_maps_yandex_net_vla) |
| Testing | Default | [core-jams-rdr-cache.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-rdr-cache.testing.maps.yandex.net/) | [core-jams-rdr-cache.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-rdr-cache.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-jams-rdr-cache-testing-maps;signal=service_total) | [rtc_balancer_core-jams-rdr-cache_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache_testing_maps_yandex_net_sas)<br>[rtc_balancer_core-jams-rdr-cache_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache_testing_maps_yandex_net_vla) |
| Testing | Internal | [core-jams-rdr-cache-internal.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-rdr-cache-internal.testing.maps.yandex.net/) | [core-jams-rdr-cache-internal.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-rdr-cache-internal.testing.maps.yandex.net;itype=balancer;locations=sas,vla;prj=core-jams-rdr-cache-internal-testing-balancer;signal=service_total/) | [rtc_balancer_core-jams-rdr-cache_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache-internal_testing_maps_yandex_net_sas)<br>[rtc_balancer_core-jams-rdr-cache_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-rdr-cache-internal_testing_maps_yandex_net_vla) |

В production балансере используется нестандартный метод балансировки запросов: [hashing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-rdr-hist.maps.yandex.net/upstreams/list/default/show/).
Таким образом мы отправляем запросы одинаковых тайлов на одни и те же backend'ы, за счет чего увечиваем cache hit и, следовательно, производительность всего кластера примерно в полтора раза.
## What happens when service is down

Пробки и дорожные события на карте не отображаются или отображаются некорректно.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-jams-rdr-cache.maps.yandex.net' |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Known clients

[Maps-mobile](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mobile/) <br>
[Maps.API](https://tech.yandex.com/maps/) <br>
[Yandex Maps](http://maps.yandex.ru)


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_jams_rdr_cache) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_jams_rdr_cache.py)


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_JAMS_RDR_CACHE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_RDR_CACHE_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_JAMS_RDR_CACHE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_RDR_CACHE_TESTING_RTC_NETS_ ) |
| load | [ \_MAPS_CORE_JAMS_RDR_CACHE_LOAD_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_RDR_CACHE_LOAD_RTC_NETS_ ) |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Тикет | https://st.yandex-team.ru/MAPSJAMS-3221 |
| Lunapark | https://lunapark.yandex-team.ru/regress/MAPSJAMS?service=jams_rdr_cache |                                                    |
| Тайминги | https://sandbox.yandex-team.ru/scheduler/21921/view |
| Разладка | https://sandbox.yandex-team.ru/scheduler/21906/view |
