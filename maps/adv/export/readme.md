# Экспорт рекламных кампаний

Генерит xml для баннерокрутилки
Говорит, есть вот такие кампании, показывай как хочешь.
Баннерокрутилка забирает xml каждые 2-5 минут. В ней список всех активных кампаний.

## General information
| What | Who |
| ---- | --- |
| Ответственные | maps-adv-dev@yandex-team.ru |
| Исходники | [maps/adv/export](https://a.yandex-team.ru/arc/trunk/arcadia/maps/adv/export) |
| Сервис в ABC | [maps-adv-export](https://abc.yandex-team.ru/services/maps-adv-export/)|
| CI (TestEnv) - Покоммитный | [BUILD\_DOCKER\_MAPS\_ADV\_EXPORT](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_ADV_EXPORT)|


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps\_adv\_export\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_export_prestable/) | [ adv-export.prestable ](https://yasm.yandex-team.ru/template/panel/maps-adv-export-prestable-panel-main/) | [ maps\_adv\_export\_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_export_prestable) |
| Stable | [maps\_adv\_export\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_export_stable/) | [ adv-export.stable ](https://yasm.yandex-team.ru/template/panel/maps-adv-export-stable-panel-main/) | [ maps\_adv\_export\_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_export_stable) |
| Testing | [maps\_adv\_export\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_export_testing/) | [ adv-export.testing ](https://yasm.yandex-team.ru/template/panel/maps-adv-export-testing-panel-main/) | [ maps\_adv\_export\_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_export_testing) |


[Monitorings all (tag=a\_prj\_maps-adv-export)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-adv-export)

| Staging | User panels |
| ------- | ----------- |
| TODO    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [adv-export.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-export.maps.yandex.net/) | [adv-export.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-export.maps.yandex.net;itype=balancer;ctype=prod;prj=adv-export-maps;signal=service_total) | [rtc\_balancer\_adv-export\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-export_maps_yandex_net_vla) [rtc\_balancer\_adv-export\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-export_maps_yandex_net_man) [rtc\_balancer\_adv-export\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-export_maps_yandex_net_sas)|
| Testing | Default | [adv-export.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-export.testing.maps.yandex.net/) | [adv-export.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-export.testing.maps.yandex.net;itype=balancer;ctype=prod;prj=adv-export-testing-maps;signal=service_total) | [rtc\_balancer\_adv-export\_testing\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-export_testing_maps_yandex_net_vla) [rtc\_balancer\_adv-export\_testing\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-export_testing_maps_yandex_net_man)|


## What happens when service is down

- Не применяются изменения, внесённые в РК;
- По кампаниям, которые уже попали в экспорт, продолжаются показы баннеров/пинов, даже если бюджет уже закончился (идут перекрутки).

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/export-*.log |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2021-08-01\` WHERE vhost LIKE 'adv-export.maps.yandex.net' LIMIT 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

    $ supervisorctl restart export

## Documentation

https://wiki.yandex-team.ru/geoadv/core-dev/

## Known clients
None


## SLA

TODO:
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_export_prestable/yp_pods/ |
| Sstable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_export_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_export_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS\_ADV\_EXPORT\_STABLE\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_EXPORT_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS\_ADV\_EXPORT\_TESTING\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_EXPORT_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
TODO
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???
