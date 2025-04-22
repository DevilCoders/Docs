# Maps-Core-Nmaps-Mrc-Tasksplanner
Бекенд для админки объездов Зеркал.

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Дмитрий Сухов ( quoter@yandex-team.ru )|
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/tasks-planner |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-tasksplanner/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_TASKSPLANNER |

## Instances

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_tasksplanner_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_tasksplanner_stable/) | [ core-nmaps-mrc-tasksplanner.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-tasksplanner-stable-panel-main/) | [ maps_core_nmaps_mrc_tasksplanner_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_tasksplanner_stable) |
| Testing | [maps_core_nmaps_mrc_tasksplanner_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_tasksplanner_testing/) | [ core-nmaps-mrc-tasksplanner.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-tasksplanner-testing-panel-main/) | [ maps_core_nmaps_mrc_tasksplanner_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_tasksplanner_testing) |
[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-tasksplanner)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-tasksplanner)


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | default | [core-nmaps-mrc-tasksplanner.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-tasksplanner.maps.yandex.net/) | [core-nmaps-mrc-tasksplanner.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla;fqdn=core-nmaps-mrc-tasksplanner.maps.yandex.net;prj=maps-core-nmaps-mrc-tasksplanner;signal=service_total;) | [rtc_balancer_core-nmaps-mrc-tasksplanner_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-tasksplanner_maps_yandex_net_sas) <br>[rtc_balancer_core-nmaps-mrc-tasksplanner_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-tasksplanner_maps_yandex_net_vla) |
| Testing | default | [core-nmaps-mrc-tasksplanner.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-tasksplanner.testing.maps.yandex.net/) | [core-nmaps-mrc-tasksplanner.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=man;fqdn=core-nmaps-mrc-tasksplanner.testing.maps.yandex.net;prj=core-nmaps-mrc-tasksplanner-testing-maps;signal=service_total;) | [rtc_balancer_core-nmaps-mrc-tasksplanner_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-tasksplanner_testing_maps_yandex_net_man) |
| Testing | testing | [core-nmaps-mrc-tasksplanner.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-mrc-tasksplanner.common.testing.maps.yandex.net"}) | [core-nmaps-mrc-tasksplanner.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-nmaps-mrc-tasksplanner_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |

### Racktables network macros
- Stable: https://racktables.yandex-team.ru/index.php?page=file&file_id=47760

- Testing: https://racktables.yandex-team.ru/index.php?page=file&file_id=63406


## Documentation

https://wiki.yandex-team.ru/jandekskarty/projects/catalog/ek/ek-nk/projects/automnyak/main/tasks-planner/vision-scope/

https://wiki.yandex-team.ru/jandekskarty/projects/catalog/ek/ek-nk/projects/automnyak/main/tasks-planner/architecture/

## Known clients

UI:
- stable https://mrc-planner.c.maps.yandex.ru
- testing https://mrc-planner.tst.c.maps.yandex-team.ru


## What happens when service is down
Админка объездов (внутренний инструмент) перестает работать.


## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| DoBlu Agent | /var/log/yandex/geo-dorblu-agent/* |
| Yacare| /var/log/yandex/maps/yacare/* |
| Fastcgi | /var/log/yandex/maps/mrc-tasks-planner/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : select * from hahn.[home/logfeller/logs/maps-log/1d/2018-02-28] where tskv_format='mrc-tasks-planner' (сюда упадут ВСЕ логи - фильтруйте по полю source_uri) |

## Ecstatic Datasets
| Stable | Testing |
| ------ | ------- |
| [yandex-maps-graph-activator](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-activator/versions) | [yandex-maps-graph-activator](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-activator/versions) |
| [yandex-maps-graph-compact](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-compact/versions) | [yandex-maps-graph-compact](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-compact/versions) |
| [yandex-maps-graph-compact-edges-persistent-index](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-compact-edges-persistent-index/versions) | [yandex-maps-graph-compact-edges-persistent-index](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-compact-edges-persistent-index/versions) |
| [yandex-maps-graph-compact-rtree](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-compact-rtree/versions) | [yandex-maps-graph-compact-rtree](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-compact-rtree/versions) |
| [yandex-maps-mrc-pedestrian-graph-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph-pro/versions) | [yandex-maps-mrc-pedestrian-graph-pro](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph-pro/versions) |

## Regression Stress Testing Configurations

