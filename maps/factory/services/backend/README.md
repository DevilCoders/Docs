# Maps Core Factory Backend

## General information

| What | Who |
| ---- | --- |
| Responsible | [Dmitry Sukhov](https://staff.yandex-team.ru/quoter), [Nikolai Fedorov](https://staff.yandex-team.ru/unril), [Roman Sokolov](https://staff.yandex-team.ru/resokolov)|
| Responsible SRE |  |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/backend |
| ABC service | https://abc.yandex-team.ru/services/maps-core-factory-backend/ |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_backend_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_backend_stable/) | [ core-factory-backend.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-backend-stable-panel-main/) | [ maps_core_factory_backend_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_backend_stable) |
| Testing | [maps_core_factory_backend_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_backend_testing/) | [ core-factory-backend.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-backend-testing-panel-main/) | [ maps_core_factory_backend_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_backend_testing) |

[Monitorings all (tag=a_prj_maps-core-factory-backend)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-backend)

[Ratelimiter panel](https://yasm.yandex-team.ru/template/panel/maps_core_factory_backend-ratelimiter2-panel)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-factory-backend.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-backend.maps.yandex.net/) | [core-factory-backend.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-backend.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=core-factory-backend-maps;signal=service_total) | [rtc_balancer_core-factory-backend_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-backend_maps_yandex_net_man)<br>[rtc_balancer_core-factory-backend_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-backend_maps_yandex_net_sas)<br>[rtc_balancer_core-factory-backend_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-backend_maps_yandex_net_vla) |
| Testing | Default | [core-factory-backend.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-backend.testing.maps.yandex.net/) | [core-factory-backend.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-backend.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-factory-backend-testing-maps;signal=service_total) | [rtc_balancer_core-factory-backend_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-backend_testing_maps_yandex_net_sas) |

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/core-factory-backend/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`//home/logfeller/logs/maps-log/1d/2020-09-12` WHERE vhost='core-factory-backend.maps.yandex.net'```|

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## How to start instaince in development

For example, commands to run servant in testing environment would be follows:

```
$ ya make
$ YCR_MODE=http:8080 ENVIRONMENT_NAME=testing ./bin/factory-backend --secret-version sec-01ctr01yff229jm9a0e6y78hpt --ignore-check-yacare-config
```

## Known clients

## SLA

## Persistent Volumes

/logs - symlink from /var/log

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FACTORY_BACKEND_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_BACKEND_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FACTORY_BACKEND_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_BACKEND_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
