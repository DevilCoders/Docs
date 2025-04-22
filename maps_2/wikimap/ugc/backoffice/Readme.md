# Core Ugc Backoffice

[**Бэкофис Maps UGC Account**](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Backoffice.md) - часть [**Maps UGC Account**](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Readme.md), предназначенная для межсервисного взаимодействия: из пользовательского ui запросы сюда не приходят.



## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Анна Ждан (likynushka@yandex-team.ru)  <br> Алексей Пономарев (ponomarev@yandex-team.ru)|
| Отвественные SRE | Анна Ждан (likynushka@yandex-team.ru)  <br> Алексей Пономарев (ponomarev@yandex-team.ru)  <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/ugc/backoffice](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/backoffice) |
| Сервис в ABC | [maps-core-ugc-backoffice](https://abc.yandex-team.ru/services/maps-core-ugc-backoffice/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_UGC_BACKOFFICE |


## Service infrastructure

### Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

Environment  | TVM Application ID
-------------|-------------------
testing      | [2025132](https://abc.yandex-team.ru/services/maps-core-ugc-backoffice/resources/)
production   | [2025130](https://abc.yandex-team.ru/services/maps-core-ugc-backoffice/resources/)

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_ugc_backoffice_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_backoffice_stable/) | [ core-ugc-backoffice.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-ugc-backoffice-stable-panel-main/) | [ maps_core_ugc_backoffice_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ugc_backoffice_stable) |
| Testing | [maps_core_ugc_backoffice_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_backoffice_testing/) | [ core-ugc-backoffice.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-ugc-backoffice-testing-panel-main/) | [ maps_core_ugc_backoffice_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_ugc_backoffice_testing) |


[Monitorings all (tag=a_prj_maps-core-ugc-backoffice)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-ugc-backoffice)

| Staging | User panels |
| ------- | ----------- |
| ????    | ?????       |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-ugc-backoffice.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ugc-backoffice.maps.yandex.net/) | [core-ugc-backoffice.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-ugc-backoffice.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,man,sas;prj=core-ugc-backoffice-maps;signal=service_total) | [rtc_balancer_core-ugc-backoffice_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ugc-backoffice_maps_yandex_net_man)<br>[rtc_balancer_core-ugc-backoffice_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ugc-backoffice_maps_yandex_net_sas)<br>[rtc_balancer_core-ugc-backoffice_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ugc-backoffice_maps_yandex_net_vla) |
| Testing | Default | [core-ugc-backoffice.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-ugc-backoffice.testing.maps.yandex.net/) | [core-ugc-backoffice.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-ugc-backoffice.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-ugc-backoffice-testing-maps;signal=service_total) | [rtc_balancer_core-ugc-backoffice_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-ugc-backoffice_testing_maps_yandex_net_sas) |

## What happens when service is down

В ленту в личном кабинете карта не добавляются новые данные, не удаётся получить информацию об этих данных.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-ugc-backoffice.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис

## Как выкатить сервис

При выкатке нужно помнить про совместимость с [account](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/account). В некоторых ситуациях может быть важен порядок выкатки этих сервисов

1. Выкатить миграцию в тестинг. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/migrations/README.md) по выкатке
2. Выкатить сервис в тестинг. [Документация sedem-а](https://docs.yandex-team.ru/sedem/releases)
3. Проверить, что работает загрузка данных в личный кабинет. Например, можно оставить фидбек на карту/фотографии в [тестинге](https://l7test.yandex.ru/maps/profile/ugc/photos) и увидеть их в ЛК.
4. Убедиться, что работают стрельбы. [Документация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/prepare_ammo/Readme.md) по стрельбам. Для backoffice стрельбы приходится запускать вручную, т.к. там происходит запись в бд
5. Выкатить миграцию в прод. [Инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/migrations/README.md) по выкатке
6. Выкатить сервис в прод

## Documentation

Форматы и документация [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Readme.md).

## Known clients
- https://abc.yandex-team.ru/services/maps-core-feedback-api/
- https://abc.yandex-team.ru/services/maps-core-photos
- https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/
- https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-lt

Все клиенты отражены в [конфиге ratelimiter-а](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_ugc_backoffice/)


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_backoffice_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_ugc_backoffice_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_UGC_BACKOFFICE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_UGC_BACKOFFICE_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_UGC_BACKOFFICE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_UGC_BACKOFFICE_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/NMAPS-13013
    * Тикет: https://st.yandex-team.ru/NMAPS-13013
    * Документация про стрельбы [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/prepare_ammo/Readme.md)

