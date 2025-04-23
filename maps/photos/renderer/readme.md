# Core Pht Renderer

Отдает тайлы и хотспоты фотослоя. Данные фотослоя приносятся датасетом yandex-maps-spots-pht-mmsrenderer.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Отвественные SRE | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Исходники | [maps/photos/renderer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/photos/renderer) |
| Сервис в ABC | [maps-core-pht-renderer](https://abc.yandex-team.ru/services/maps-core-pht-renderer/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_PHT_RENDERER |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Load | [maps_core_pht_renderer_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_renderer_load/) | [ core-pht-renderer.load ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-renderer-load-panel-main/) | [ maps_core_pht_renderer_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_renderer_load) |
| Prestable | [maps_core_pht_renderer_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_renderer_prestable/) | [ core-pht-renderer.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-renderer-prestable-panel-main/) | [ maps_core_pht_renderer_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_renderer_prestable) |
| Stable | [maps_core_pht_renderer_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_renderer_stable/) | [ core-pht-renderer.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-renderer-stable-panel-main/) | [ maps_core_pht_renderer_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_renderer_stable) |
| Testing | [maps_core_pht_renderer_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_pht_renderer_testing/) | [ core-pht-renderer.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-pht-renderer-testing-panel-main/) | [ maps_core_pht_renderer_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_pht_renderer_testing) |


[Monitorings all (tag=a_prj_maps-core-pht-renderer)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-pht-renderer)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-pht-renderer.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-pht-renderer.maps.yandex.net/) | [core-pht-renderer.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-pht-renderer.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-pht-renderer-maps;signal=service_total) | [rtc_balancer_core-pht-renderer_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-renderer_maps_yandex_net_man)<br>[rtc_balancer_core-pht-renderer_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-renderer_maps_yandex_net_sas)<br>[rtc_balancer_core-pht-renderer_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-pht-renderer_maps_yandex_net_vla) |
| Testing | Common | [core-pht-renderer.testing.maps.n.yandex.ru](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-pht-renderer-testing-slb) | [core-pht-renderer.testing.maps.n.yandex.ru](https://yasm.yandex-team.ru/template/panel/dynbalancer_common_panel/section=maps-core-pht-renderer-testing-slb/)


## What happens when service is down

Перестанут отображаться тайлы фотослоя на БЯК/МЯК
Перестанут обрабатываться клики на фотослой в БЯК/МЯК

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/pht_renderer/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-pht-renderer.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Откатить датасет.

Рестартовать сервис: sudo yacare restart pht-renderer

## Known clients
- БЯК maps.yandex.ru
- МЯК


## Ecstatic Datasets

| Stable | Testing |
| ------ | ------- |
| [yandex-maps-spots-pht-mmsrenderer](http://ecstatic.maps.yandex.net/pkg/yandex-maps-spots-pht-mmsrenderer/versions) | [yandex-maps-spots-pht-mmsrenderer](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-spots-pht-mmsrenderer/versions) |


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_pht_renderer) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_pht_renderer.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /var/lib/yandex/maps/pht_renderer - активированные версии датасета с данными карт
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_PHT_RENDERER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PHT_RENDERER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_PHT_RENDERER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PHT_RENDERER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSNAVI?service=pht_renderer
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/15640, https://sandbox.yandex-team.ru/scheduler/15644
    * Тикет: https://st.yandex-team.ru/MAPSNAVI-3503
