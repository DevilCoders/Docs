# Core Factory Sputnica Backend

Рендерер тайлов для [Спутницы](https://sputnica.yandex.ru).

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE | Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | [maps/factory/services/sputnica_back](https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/sputnica_back) |
| Сервис в ABC | [maps-core-factory-sputnica-back](https://abc.yandex-team.ru/services/maps-core-factory-sputnica-back/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_FACTORY_SPUTNICA_BACK |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_sputnica_back_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_sputnica_back_stable/) | [ core-factory-sputnica-back.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-sputnica-back-stable-panel-main/) | [ maps_core_factory_sputnica_back_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_sputnica_back_stable) |
| Testing | [maps_core_factory_sputnica_back_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_sputnica_back_testing/) | [ core-factory-sputnica-back.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-sputnica-back-testing-panel-main/) | [ maps_core_factory_sputnica_back_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_sputnica_back_testing) |

[Monitorings all (tag=a_prj_maps-core-factory-sputnica-back)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-sputnica-back)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-factory-sputnica-back.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-sputnica-back.maps.yandex.net/) | [core-factory-sputnica-back.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-sputnica-back.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-factory-sputnica-back-maps;signal=service_total) | [rtc_balancer_core-factory-sputnica-back_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-sputnica-back_maps_yandex_net_man)<br>[rtc_balancer_core-factory-sputnica-back_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-sputnica-back_maps_yandex_net_sas)<br>[rtc_balancer_core-factory-sputnica-back_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-sputnica-back_maps_yandex_net_vla) |
| Testing | Default | [core-factory-sputnica-back.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-sputnica-back.testing.maps.yandex.net/) | [core-factory-sputnica-back.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-sputnica-back.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-factory-sputnica-back-testing-maps;signal=service_total) | [rtc_balancer_core-factory-sputnica-back_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-sputnica-back_testing_maps_yandex_net_sas) |

## What happens when service is down

TODO: Напишите, что происходит при отказе сервиса

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/factory-sputnica-back/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`//home/logfeller/logs/maps-log/1d/2019-10-12` WHERE vhost='core-factory-sputnica-back'.maps.yandex.net'``` |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

TODO: Добавьте ссылки на Wiki и другие описания (если есть)

## Known clients

- TODO: Сюда напишите список известных клиентов
- ????

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

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FACTORY_SPUTNICA_BACK_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_SPUTNICA_BACK_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FACTORY_SPUTNICA_BACK_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_SPUTNICA_BACK_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations

* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???
