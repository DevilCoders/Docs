# Точечница

Занимается отдачей полигонов для организаций
## General information
| What | Who |
| ---- | --- |
| Ответственные | maps-adv-dev@yandex-team.ru |
| Исходники | [maps/adv/points/server](https://a.yandex-team.ru/arc/trunk/arcadia/maps/adv/points/server) |
| Сервис в ABC | [maps-adv-points](https://abc.yandex-team.ru/services/maps-adv-points/)|
| CI (TestEnv) - Покоммитный | [BUILD\_DOCKER\_MAPS\_ADV\_POINTS](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_ADV_POINTS)|


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Testing | [maps\_adv\_points\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_points_testing/) | [ adv-points.testing ](https://yasm.yandex-team.ru/template/panel/maps-adv-points-testing-panel-main/) | [ maps\_adv\_points\_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_points_testing) |
| Prestable | [maps\_adv\_points\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_points_prestable/) | [ adv-points.prestable ](https://yasm.yandex-team.ru/template/panel/maps-adv-points-prestable-panel-main/) | [ maps\_adv\_points\_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_points_prestable) |
| Stable | [maps\_adv\_points\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_points_stable/) | [ adv-points.stable ](https://yasm.yandex-team.ru/template/panel/maps-adv-points-stable-panel-main/) | [ maps\_adv\_points\_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_points_stable) |


[Monitorings all (tag=a\_prj\_maps-adv-points)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-adv-points)

| Staging | User panels |
| ------- | ----------- |
| TODO    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Testing | Default | [adv-points.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-points.testing.maps.yandex.net/) | [adv-points.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-points.testing.maps.yandex.net;itype=balancer;ctype=prod;prj=adv-points-testing-maps;signal=service_total) | [rtc\_balancer\_adv-points\_testing\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-points_testing_maps_yandex_net_vla) [rtc\_balancer\_adv-points\_testing\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-points_testing_maps_yandex_net_man)|
| Stable | Default | [adv-points.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-points.maps.yandex.net/) | [adv-points.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-points.maps.yandex.net;itype=balancer;ctype=prod;prj=adv-points-maps;signal=service_total) | [rtc\_balancer\_adv-points\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-points_maps_yandex_net_vla) [rtc\_balancer\_adv-points\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-points_maps_yandex_net_man)|


## What happens when service is down

Не работает прогноз по РК (Медиапланирование в Агентском кабинете).
Также перестаёт обновляться экспорт рекламных кампаний (РК), из-за чего:
- не применяются изменения, внесённые в РК;
- по кампаниям, которые уже попали в экспорт, продолжаются показы баннеров/пинов, даже если бюджет уже закончился (идут перекрутки).

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/points-*.log |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2021-08-01\` WHERE vhost LIKE 'adv-points.maps.yandex.net' LIMIT 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

    $ supervisorctl restart points

## Documentation

https://wiki.yandex-team.ru/geoadv/core-dev/

## Known clients
- Экспорт рекламных кампаний (maps-adv-export)
- Агентский кабинет

## SLA

TODO:
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_points_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_points_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_points_stable/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS\_ADV\_POINTS\_STABLE\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_POINTS_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS\_ADV\_POINTS\_TESTING\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_POINTS_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
TODO
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???
