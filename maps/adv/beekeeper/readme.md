# Пчеловод

Перекладывает события в несколько таблиц в кликхаусе.
В финале считает, сколько денег должны списать.
За показы / за клики / etc.
Дальше через billing proxy идёт в баланс.
Если лимит показов исчерпан, кампания останавливается.

## General information
| What | Who |
| ---- | --- |
| Ответственные | maps-adv-dev@yandex-team.ru |
| Исходники | [maps/adv/beekeeper](https://a.yandex-team.ru/arc/trunk/arcadia/maps/adv/beekeeper) |
| Сервис в ABC | [maps-adv-statistics](https://abc.yandex-team.ru/services/maps-adv-statistics/)|
| CI (TestEnv) - Покоммитный | [BUILD\_DOCKER\_MAPS\_ADV\_BEEKEEPER](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_ADV_BEEKEEPER) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps\_adv\_beekeeper\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_beekeeper_prestable/) | [ adv-beekeeper.prestable ](https://yasm.yandex-team.ru/template/panel/maps-adv-beekeeper-prestable-panel-main/) | [ maps\_adv\_beekeeper\_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_beekeeper_prestable) |
| Stable | [maps\_adv\_beekeeper\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_beekeeper_stable/) | [ adv-beekeeper.stable ](https://yasm.yandex-team.ru/template/panel/maps-adv-beekeeper-stable-panel-main/) | [ maps\_adv\_beekeeper\_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_beekeeper_stable) |
| Testing | [maps\_adv\_beekeeper\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_beekeeper_testing/) | [ adv-beekeeper.testing ](https://yasm.yandex-team.ru/template/panel/maps-adv-beekeeper-testing-panel-main/) | [ maps\_adv\_beekeeper\_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_beekeeper_testing) |


[Monitorings all (tag=a\_prj\_maps-adv-beekeeper)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-adv-beekeeper)

| Staging | User panels |
| ------- | ----------- |
| ????    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [adv-beekeeper.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-beekeeper.maps.yandex.net/) | [adv-beekeeper.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-beekeeper.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=adv-beekeeper-maps;signal=service_total) | [rtc\_balancer\_adv-beekeeper\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-beekeeper_maps_yandex_net_man)<br>[rtc\_balancer\_adv-beekeeper\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-beekeeper_maps_yandex_net_sas)<br>[rtc\_balancer\_adv-beekeeper\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-beekeeper_maps_yandex_net_vla) |
| Testing | Default | [adv-beekeeper.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-beekeeper.testing.maps.yandex.net/) | [adv-beekeeper.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-beekeeper.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas;prj=adv-beekeeper-testing-maps;signal=service_total) | [rtc\_balancer\_adv-beekeeper\_testing\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-beekeeper_testing_maps_yandex_net_man)<br>[rtc\_balancer\_adv-beekeeper\_testing\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-beekeeper_testing_maps_yandex_net_sas) |


## What happens when service is down

Перестаёт считаться статистика, происходят перекрутки, не останавливаются рекламные кампании.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/beekeeper-*.log |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2021-08-01` WHERE vhost LIKE 'adv-beekeeper.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

    $ supervisorctl restart beekeeper

## Documentation

https://wiki.yandex-team.ru/geoadv/core-dev/

## Known clients
None

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_beekeeper_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_beekeeper_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_beekeeper_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS\_ADV\_BEEKEEPER\_STABLE\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_BEEKEEPER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS\_ADV\_BEEKEEPER\_TESTING\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_BEEKEEPER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???
