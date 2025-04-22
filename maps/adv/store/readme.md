# Хранилище рекламных кампаний

Предоставляет АПИ, чтобы создавать рекламные кампании, задаёт поведение баннера и пр

## General information
| What | Who |
| ---- | --- |
| Ответственные | maps-adv-dev@yandex-team.ru |
| Исходники | [maps/adv/store](https://a.yandex-team.ru/arc/trunk/arcadia/maps/adv/store) |
| Сервис в ABC | [maps-adv-store](https://abc.yandex-team.ru/services/maps-adv-store/)|
| CI (TestEnv) - Покоммитный | [BUILD\_DOCKER\_MAPS\_ADV\_STORE](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_ADV_STORE) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps\_adv\_store\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_store_prestable/) | [ adv-store.prestable ](https://yasm.yandex-team.ru/template/panel/maps-adv-store-prestable-panel-main/) | [ maps\_adv\_store\_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_store_prestable) |
| Stable | [maps\_adv\_store\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_store_stable/) | [ adv-store.stable ](https://yasm.yandex-team.ru/template/panel/maps-adv-store-stable-panel-main/) | [ maps\_adv\_store\_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_store_stable) |
| Testing | [maps\_adv\_store\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_store_testing/) | [ adv-store.testing ](https://yasm.yandex-team.ru/template/panel/maps-adv-store-testing-panel-main/) | [ maps\_adv\_store\_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_store_testing) |


[Monitorings all (tag=a\_prj\_maps-adv-store)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-adv-store)

| Staging | User panels |
| ------- | ----------- |
| ????    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Testing | Default | [adv-store.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-store.testing.maps.yandex.net/) | [adv-store.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-store.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla;prj=adv-store-testing-maps;signal=service_total) | [rtc\_balancer\_adv-store\_testing\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-store_testing_maps_yandex_net_man)<br>[rtc\_balancer\_adv-store\_testing\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-store_testing_maps_yandex_net_vla) |
| Stable | Default | [adv-store.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-store.maps.yandex.net/) | [adv-store.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-store.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla;prj=adv-store-maps;signal=service_total) | [rtc\_balancer\_adv-store\_testing\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-store_maps_yandex_net_man)<br>[rtc\_balancer\_adv-store\_testing\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-store_maps_yandex_net_sas)<br>[rtc\_balancer\_adv-store\_testing\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-store_maps_yandex_net_vla) |


## What happens when service is down

В агентском кабинете нельзя будет создать новые рекламные кампании или изменить существующие, а так же посмотреть статистику по кампаниям.
Перестанет генерироваться экспорт кампаний (может привести к перекруткам)

Разломается ещё подсчёт статистики в бикипере.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/store-*.log |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2021-08-01\` WHERE vhost LIKE 'adv-store.maps.yandex.net' LIMIT 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

    $ supervisorctl restart store

## Documentation

https://wiki.yandex-team.ru/geoadv/core-dev/

## Known clients
- Экспорт рекламных кампаний (maps-adv-export)
- Агентский кабинет

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_store_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_store_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_store_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS\_ADV\_STORE\_STABLE\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_STORE_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS\_ADV\_STORE\_TESTING\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_STORE_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???
