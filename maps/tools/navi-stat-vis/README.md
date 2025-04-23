# Core Navi Stat Vis
Стенд предназначен для визуализации поездок пользователей поездок пользователей на основании данных из метричных таблиц.
Как частый случай использования - ссылки на визуализацию поездок в тасках в очереди [MAPKITSIM](https://st.yandex-team.ru/MAPKITSIM/order:updated:false/filter?resolution=empty())

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Александр Любицкий (innocent@yandex-team.ru) <br> Пётр Гриневич (grinev@yandex-team.ru) |
| Отвественные SRE | Александр Любицкий (innocent@yandex-team.ru) <br> Пётр Гриневич (grinev@yandex-team.ru) |
| Исходники | [maps/tools/navi-stat-vis](https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/navi-stat-vis) |
| Сервис в ABC | [maps-core-navi-stat-vis](https://abc.yandex-team.ru/services/maps-core-navi-stat-vis/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=UILD_DOCKER_MAPS_CORE_NAVI_STAT_VIS |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_navi_stat_vis_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_navi_stat_vis_stable/) | [ core-navi-stat-vis.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-navi-stat-vis-stable-panel-main/) | [ maps_core_navi_stat_vis_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_navi_stat_vis_stable) |

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-navi-stat-vis.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-navi-stat-vis.maps.yandex.net/) | [core-navi-stat-vis.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-navi-stat-vis.maps.yandex.net;itype=balancer;ctype=prod;locations=msk;prj=core-navi-stat-vis-maps;signal=service_total) | [rtc_balancer_core-navi-stat-vis_maps_yandex_net_iva](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-navi-stat-vis_maps_yandex_net_iva)<br>[rtc_balancer_core-navi-stat-vis_maps_yandex_net_myt](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-navi-stat-vis_maps_yandex_net_myt) |


## What happens when service is down

Перестанет работать визуализатор пользовательских треков

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NAVI_STAT_VIS_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NAVI_STAT_VIS_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NAVI_STAT_VIS_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NAVI_STAT_VIS_TESTING_RTC_NETS_ ) |

## Доступ к сервису ##

Доступ к сервису регулируется через роль Разработчик в сервисе [Пользователи стенда maps-core-navi-stat-vis](https://abc.yandex-team.ru/services/maps-core-navi-stat-vis-users/)
