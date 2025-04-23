# Манул

*от англ. manual ручной* - сервис для ручных (бесплатных, платных) заказов.

Биллинг прокси работает с балансом. Есть заказы, которые не хочется проводить через биллинг.
Принесли миллион - делаем хорошо за миллион. Не учитывает деньги.

## General information
| What | Who |
| ---- | --- |
| Ответственные | maps-adv-dev@yandex-team.ru |
| Исходники | [maps/adv/manul](https://a.yandex-team.ru/arc/trunk/arcadia/maps/adv/manul) |
| Сервис в ABC | [maps-adv-manul](https://abc.yandex-team.ru/services/maps-adv-manul/)|
| CI (TestEnv) - Покоммитный | [BUILD\_DOCKER\_MAPS\_ADV\_MANUL](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_ADV_MANUL) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps\_adv\_manul\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_manul_prestable/) | [ adv-manul.prestable ](https://yasm.yandex-team.ru/template/panel/maps-adv-manul-prestable-panel-main/) | [ maps\_adv\_manul\_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_manul_prestable) |
| Stable | [maps\_adv\_manul\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_manul_stable/) | [ adv-manul.stable ](https://yasm.yandex-team.ru/template/panel/maps-adv-manul-stable-panel-main/) | [ maps\_adv\_manul\_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_manul_stable) |
| Testing | [maps\_adv\_manul\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_manul_testing/) | [ adv-manul.testing ](https://yasm.yandex-team.ru/template/panel/maps-adv-manul-testing-panel-main/) | [ maps\_adv\_manul\_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_manul_testing) |


[Monitorings all (tag=a\_prj\_maps-adv-manul)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-adv-manul)

| Staging | User panels |
| ------- | ----------- |
| TODO    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [adv-manul.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-manul.maps.yandex.net/) | [adv-manul.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-manul.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas;prj=adv-manul-maps;signal=service_total) | [rtc\_balancer\_adv-manul\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-manul_maps_yandex_net_sas)<br>[rtc\_balancer\_adv-manul\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-manul_maps_yandex_net_man)<br>[rtc\_balancer\_adv-manul\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-manul_maps_yandex_net_vla) |
| Testing | Default | [adv-manul.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-manul.testing.maps.yandex.net/) | [adv-manul.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-manul.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas;prj=adv-manul-testing-maps;signal=service_total) | [rtc\_balancer\_adv-manul\_testing\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-manul_testing_maps_yandex_net_sas)<br>[rtc\_balancer\_adv-manul\_testing\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-manul_testing_maps_yandex_net_vla) |


## What happens when service is down

В агентском кабинете нельзя будет создать новые ручные заказы или изменить существующие.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/manul-*.log |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2021-08-01\` WHERE vhost LIKE 'adv-manul.maps.yandex.net' LIMIT 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

    $ supervisorctl restart manul

## Documentation

https://wiki.yandex-team.ru/geoadv/core-dev/

## Known clients
- Агентский кабинет (front-pins-agency-cabinet)

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_manul_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_manul_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_manul_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS\_ADV\_MANUL\_STABLE\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_MANUL_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS\_ADV\_MANUL\_TESTING\_RTC\_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_MANUL_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???

