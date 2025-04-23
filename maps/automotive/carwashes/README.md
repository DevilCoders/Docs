# [DELETED] Auto Navi Carwashes

Сервис для покупки услуги мойки авто в навигаторе

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Куприянов (kupriyanov-m@yandex-team.ru) |
| Отвественные SRE | Михаил Куприянов (kupriyanov-m@yandex-team.ru), Михаил Крутяков (mkrutyakov@yandex-team.ru) |
| Исходники | [maps/automotive/carwashes](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/carwashes) |
| Сервис в ABC | [maps-auto-navi-carwashes](https://abc.yandex-team.ru/services/maps-auto-navi-carwashes/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_NAVI_CARWASHES |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_auto_navi_carwashes_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_prestable/) | [ auto-navi-carwashes.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-carwashes-prestable-panel-main/) | [ maps_auto_navi_carwashes_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_carwashes_prestable) |
| Stable | [maps_auto_navi_carwashes_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_stable/) | [ auto-navi-carwashes.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-carwashes-stable-panel-main/) | [ maps_auto_navi_carwashes_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_carwashes_stable) |
| Stress | [maps_auto_navi_carwashes_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_stress/) | [ auto-navi-carwashes.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-carwashes-stress-panel-main/) | [ maps_auto_navi_carwashes_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_carwashes_stress) |
| Testing | [maps_auto_navi_carwashes_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_testing/) | [ auto-navi-carwashes.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-carwashes-testing-panel-main/) | [ maps_auto_navi_carwashes_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_carwashes_testing) |


[Monitorings all (tag=a_prj_maps-auto-navi-carwashes)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-navi-carwashes)

**Ratelimiter panel:** [RPS and Quotas](https://yasm.yandex-team.ru/template/panel/maps_auto_navi_carwashes-ratelimiter2-panel/)

**MDB monitorings**

| Staging | Graphics panel |
| ------- | -------------- |
| Stable | [maps-auto-navi-carwashes-stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbdr3cdm6lk53geret5) |
| Testing | [maps-auto-navi-carwashes-testing](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbh9vgk1vivrqi0r1is) |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [auto-navi-carwashes.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-navi-carwashes.maps.yandex.net/) | [auto-navi-carwashes.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-navi-carwashes.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=auto-navi-carwashes-maps;signal=service_total) | [rtc_balancer_auto-navi-carwashes_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-carwashes_maps_yandex_net_man)<br>[rtc_balancer_auto-navi-carwashes_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-carwashes_maps_yandex_net_sas)<br>[rtc_balancer_auto-navi-carwashes_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-carwashes_maps_yandex_net_vla) |
| Testing | Default | [auto-navi-carwashes.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-navi-carwashes.testing.maps.yandex.net/) | [auto-navi-carwashes.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-navi-carwashes.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=auto-navi-carwashes-testing-maps;signal=service_total) | [rtc_balancer_auto-navi-carwashes_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-carwashes_testing_maps_yandex_net_man)<br>[rtc_balancer_auto-navi-carwashes_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-carwashes_testing_maps_yandex_net_sas)<br>[rtc_balancer_auto-navi-carwashes_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-carwashes_testing_maps_yandex_net_vla) |


## What happens when service is down

Пользователи навигатора не смогут приобрести новые купоны на мойку (ранее приобретенные будут доступны через Datasync).
Нельзя будет произвести отмену заказа и возврат средств (которые приходят через запрос в саппорт).


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-carwashes/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'auto-carwashes.maps.yandex.net' limit 1; |


## How to fix common problems
* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
* [Ratelimiter alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2/agent_troubleshooting.md)

## Documentation

Общее описание:
https://wiki.yandex-team.ru/automotive/serverdevelopment/mojjki/

## Known clients

- IDM - ограничение доступа к сценарию возврата
- Яндекс.Формы - триггер возврата
- Startrek - содержит результаты процедуры возврата

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_stable/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_stress/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_carwashes_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_NAVI_CARWASHES_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_NAVI_CARWASHES_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_NAVI_CARWASHES_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_NAVI_CARWASHES_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/YCARBACKEND?service=maps-auto-navi-carwashes
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/25449/view, https://sandbox.yandex-team.ru/scheduler/25445/view
    * Тикет: https://st.yandex-team.ru/YCARBACKEND-603, https://st.yandex-team.ru/YCARBACKEND-602

