# Grinder

Распределяет длинные задачи:
- async_takeout_data_erasure
- async_takeout_uploader
- tasks_gen
- yt_features_exporter

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Андрей Лизунов (anlizev@yandex-team.ru), Михаил Плоткин (miplot@yandex-team.ru), Андрей Наплавков (naplavkov@yandex-team.ru), Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE | Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/grinder |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-grinder/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_GRINDER |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_grinder_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_grinder_stable/) | [ core-nmaps-mrc-grinder.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-grinder-stable-panel-main/) | [ maps_core_nmaps_mrc_grinder_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_grinder_stable) |
| Testing | [maps_core_nmaps_mrc_grinder_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_grinder_testing/) | [ core-nmaps-mrc-grinder.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-grinder-testing-panel-main/) | [ maps_core_nmaps_mrc_grinder_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_grinder_testing) |
[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-grinder)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-grinder)


### Balancers

| Staging | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | -------------- | -------------- | ----------------------- |
| Stable | [core-nmaps-mrc-grinder.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-grinder.maps.yandex.net/) | [core-nmaps-mrc-grinder.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-mrc-grinder.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas;prj=core-nmaps-mrc-grinder-maps;signal=service_total) | [rtc_balancer_core-nmaps-mrc-grinder_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-grinder_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-mrc-grinder_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-grinder_maps_yandex_net_vla) |
| Testing | [maps-core-nmaps-mrc-grinder-testing-slb](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/s.yandex-team.ru/upstreams/list/maps-core-nmaps-mrc-grinder-testing-slb/show/) | [core-nmaps-mrc-grinder.testing.maps.n.yandex.ru](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-mrc-grinder.testing.maps.n.yandex.ru;itype=balancer;ctype=test;metaprj=balancer;prj=core-nmaps-mrc-grinder-maps;signal=service_total) | [maps-core-nmaps-mrc-grinder-testing-slb](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-nmaps-mrc-grinder-testing-slb) |

## What happens when service is down

Длинные задачи перестают приниматься:
- async_takeout_data_erasure
- async_takeout_uploader
- tasks_gen
- yt_features_exporter

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/grinder/* |
| Grinder master service | /var/log/yandex/maps/mrc-grinder-master/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-nmaps-mrc-grinder.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation
- [Grinder](https://wiki.yandex-team.ru/maps/dev/core/grinder/)

## Known clients
- [Takeout](https://wiki.yandex-team.ru/passport/takeout/)
- [Планировщик объездов](https://mrc-planner.maps.yandex-team.ru/create-tasks-group)
- [Справочник организаций](https://a.yandex-team.ru/arc/trunk/arcadia/sprav/java/mapsmrc/src/main/java/ru/yandex/altay/mapsmrc/grinder/GrinderTaskDescription.java?rev=5889162#L8)

## SLA

## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_MRC_GRINDER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_GRINDER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_MRC_GRINDER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_GRINDER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
