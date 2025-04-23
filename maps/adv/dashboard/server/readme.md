# Дашборд

По запросу от кабинета, выдаёт статистику показов, кликов, ... за интервал дат по указанной РК.
По запросу от экспорта, выдаёт информацию о том, сколько уже откручено показов по указанным РК с начала дня.

## General information
| What | Who |
| ---- | --- |
| Ответственные | maps-adv-dev@yandex-team.ru |
| Исходники | [maps/adv/dashboard/server](https://a.yandex-team.ru/arc/trunk/arcadia/maps/adv/dashboard/server) |
| Сервис в ABC | [maps-adv-statistics](https://abc.yandex-team.ru/services/maps-adv-statistics/)|
| CI (TestEnv) - Покоммитный | [BUILD\_DOCKER\_MAPS\_ADV\_DASHBOARD](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_ADV_DASHBOARD) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps\_adv\_dashboard\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_dashboard_prestable/) | [ adv-dashboard.prestable ](https://yasm.yandex-team.ru/template/panel/maps-adv-dashboard-prestable-panel-main/) | [ maps\_adv\_dashboard\_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_dashboard_prestable) |
| Stable | [maps\_adv\_dashboard\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_dashboard_stable/) | [ adv-dashboard.stable ](https://yasm.yandex-team.ru/template/panel/maps-adv-dashboard-stable-panel-main/) | [ maps\_adv\_dashboard\_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_dashboard_stable) |
| Testing | [maps\_adv\_dashboard\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_dashboard_testing/) | [ adv-dashboard.testing ](https://yasm.yandex-team.ru/template/panel/maps-adv-dashboard-testing-panel-main/) | [ maps\_adv\_dashboard\_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_dashboard_testing) |


[Monitorings all (tag=a\_prj\_maps-adv-dashboard)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-adv-dashboard)

| Staging | User panels |
| ------- | ----------- |
| ????    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [adv-dashboard.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-dashboard.maps.yandex.net/) | [adv-dashboard.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-dashboard.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=adv-dashboard-maps;signal=service_total) | [rtc\_balancer\_adv-dashboard\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-dashboard_maps_yandex_net_man)<br>[rtc\_balancer\_adv-dashboard\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-dashboard_maps_yandex_net_sas)<br>[rtc\_balancer\_adv-dashboard\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-dashboard_maps_yandex_net_vla) |
| Testing | Default | [adv-dashboard.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-dashboard.testing.maps.yandex.net/) | [adv-dashboard.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-dashboard.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas;prj=adv-dashboard-testing-maps;signal=service_total) | [rtc\_balancer\_adv-dashboard\_testing\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-dashboard_testing_maps_yandex_net_man)<br>[rtc\_balancer\_adv-dashboard\_testing\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-dashboard_testing_maps_yandex_net_sas) |


## What happens when service is down

В кабинете не отображается статистика по кампаниям.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/dashboard-*.log |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2021-08-01\` WHERE vhost LIKE 'adv-dashboard.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

    $ supervisorctl restart dashboard

## Documentation

https://wiki.yandex-team.ru/geoadv/core-dev/

## Known clients
- Кабинет
- Стор
- Экспорт


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_dashboard_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_dashboard_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_dashboard_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS\_ADV\_DASHBOARD\_STABLE\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_DASHBOARD_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS\_ADV\_DASHBOARD\_TESTING\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_DASHBOARD_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???
