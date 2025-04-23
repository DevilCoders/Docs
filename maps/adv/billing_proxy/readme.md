# Биллинг прокси

Создаёт заказы в балансе, проверяет баланс на счету клиента
К заказу привязаны рекламные кампании, которые хранятся в adv-store

## General information
| What | Who |
| ---- | --- |
| Ответственные | maps-adv-dev@yandex-team.ru |
| Исходники | [maps/adv/billing\_proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/adv/billing_proxy) |
| Сервис в ABC | [maps-adv-billing](https://abc.yandex-team.ru/services/maps-adv-billing/)|
| CI (TestEnv) - Покоммитный | [BUILD\_DOCKER\_MAPS\_ADV\_BILLING\_PROXY](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_ADV_BILLING_PROXY) |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps\_adv\_billing\_proxy\_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_billing_proxy_prestable/) | [ adv-billing-proxy.prestable ](https://yasm.yandex-team.ru/template/panel/maps-adv-billing-proxy-prestable-panel-main/) | [ maps\_adv\_billing\_proxy\_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_billing_proxy_prestable) |
| Stable | [maps\_adv\_billing\_proxy\_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_billing_proxy_stable/) | [ adv-billing-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-adv-billing-proxy-stable-panel-main/) | [ maps\_adv\_billing\_proxy\_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_billing_proxy_stable) |
| Testing | [maps\_adv\_billing\_proxy\_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_billing_proxy_testing/) | [ adv-billing-proxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-adv-billing-proxy-testing-panel-main/) | [ maps\_adv\_billing\_proxy\_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_adv_billing_proxy_testing) |


[Monitorings all (tag=a\_prj\_maps-adv-billing-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-adv-billing-proxy)

| Staging | User panels |
| ------- | ----------- |
| TODO    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [adv-billing-proxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-billing-proxy.maps.yandex.net/) | [adv-billing-proxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-billing-proxy.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas;prj=adv-billing-proxy-maps;signal=service_total) | [rtc\_balancer\_adv-billing-proxy\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-billing-proxy_maps_yandex_net_man)<br>[rtc\_balancer\_adv-billing-proxy\_maps\_yandex\_net\_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-billing-proxy_maps_yandex_net_vla)<br>[rtc\_balancer\_adv-billing-proxy\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-billing-proxy_maps_yandex_net_sas) |
| Testing | Default | [adv-billing-proxy.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/adv-billing-proxy.testing.maps.yandex.net/) | [adv-billing-proxy.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=adv-billing-proxy.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas;prj=adv-billing-proxy-testing-maps;signal=service_total) | [rtc\_balancer\_adv-billing-proxy\_testing\_maps\_yandex\_net\_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-billing-proxy_testing_maps_yandex_net_man)<br>[rtc\_balancer\_adv-billing-proxy\_testing\_maps\_yandex\_net\_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_adv-billing-proxy_testing_maps_yandex_net_sas) |


## What happens when service is down

В агентском кабинете нельзя будет создать новые заказы или изменить существующие, а так же посмотреть остатки средств по заказам.
Перестанет генерироваться экспорт для рекламных кампаний и могут возникнуть перекрутки.
Перестанут отправляться запросы на списание средств по открученной рекламе.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/billing_proxy-*.log |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.\`logs/maps-log/1d/2021-08-01\` WHERE vhost LIKE 'adv-billing-proxy.maps.yandex.net' LIMIT 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

    $ supervisorctl restart billing_proxy

## Documentation

https://wiki.yandex-team.ru/geoadv/core-dev/

## Known clients
- Агентский кабинет (front-pins-agency-cabinet)
- Экспорт рекламных кампаний (maps-adv-export)
- Бикипер (maps-adv-statistics)
- Стор (maps-adv-store)

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_billing_proxy_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_billing_proxy_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_adv_billing_proxy_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS\_ADV\_BILLINGPROXY\_STABLE\_RTC\_NETS_ ](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_BILLINGPROXY_STABLE_RTC_NETS_) |
| testing | [ \_MAPS\_ADV\_BILLINGPROXY\_TESTING\_RTC\_NETS_ ](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_ADV_BILLINGPROXY_TESTING_RTC_NETS_) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???

