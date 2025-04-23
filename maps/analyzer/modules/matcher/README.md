# Core Jams Matcher

Сервис матчига сигналов.

Принимает POST запросом точку, притягивает ее к графу и отсылает, тоже POST запросом, притянутую точку и несколько предыдующих точек на один или несколько, заранее сконфигурированных URL-ов.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Александр Ручкин (voidex@yandex-team.ru), Пётр Гриневич (grinev@yandex-team.ru),  Александр Любицкий (innocent@yandex-team.ru)|
| Отвественные SRE | Александр Ручкин (voidex@yandex-team.ru), Пётр Гриневич (grinev@yandex-team.ru),  Александр Любицкий (innocent@yandex-team.ru)  |
| Исходники | [maps/analyzer/modules/matcher](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/modules/matcher) |
| Сервис в ABC | [maps-core-jams-matcher](https://abc.yandex-team.ru/services/maps-core-jams-matcher/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_JAMS_MATCHER |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_jams_matcher_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_matcher_stable/) | [ core-jams-matcher.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-matcher-stable-panel-main/) | [ maps_core_jams_matcher_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_matcher_stable) |
| Prestable | [maps_core_jams_matcher_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_matcher_prestable/) | [ core-jams-matcher.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-matcher-prestable-panel-main/) | [ maps_core_jams_matcher_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_matcher_prestable) |
| Testing | [maps_core_jams_matcher_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_matcher_testing/) | [ core-jams-matcher.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-matcher-testing-panel-main/) | [ maps_core_jams_matcher_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_matcher_testing) |
| Load | [maps_core_jams_matcher_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_matcher_load/) | [ core-jams-matcher.load ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-matcher-load-panel-main/) | [ maps_core_jams_matcher_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_matcher_load) |


[Monitorings all (tag=a_prj_maps-core-jams-matcher)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-jams-matcher)

| Staging | User panels |
| ------- | ----------- |
|     |        |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-jams-matcher.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-matcher.maps.yandex.net/) | [core-jams-matcher.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-matcher.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=core-jams-matcher-maps;signal=service_total) | [rtc_balancer_core-jams-matcher_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-matcher_maps_yandex_net_man)<br>[rtc_balancer_core-jams-matcher_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-matcher_maps_yandex_net_sas)<br>[rtc_balancer_core-jams-matcher_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-matcher_maps_yandex_net_vla) |
| Testing | Common | [core-jams-matcher.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/) | [core-jams-matcher_common_testing_maps_yandex_net_default](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=common.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=common.testing.maps.yandex.net;signal=core-jams-matcher_common_testing_maps_yandex_net_default;) | |
| Testing | Dedicated | [core-jams-matcher.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-matcher.testing.maps.yandex.net/) | [core-jams-matcher.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-jams-matcher.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man;prj=core-jams-matcher-testing-maps;signal=service_total) | [rtc_balancer_core-jams-matcher_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-matcher_testing_maps_yandex_net_man) |


## What happens when service is down

Перестанут работать отдаваться в авто координаты машин, сломается функционал парковок

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service dispatcher | /var/log/yandex/maps/dispatcher/* |
| Yacare service matcher | /var/log/yandex/maps/matcher/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`//logs/maps_core_jams_matcher_dispatcher_log/1d/2020-04-01` LIMIT 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Посмотреть логи Yacare сервисов, Ecstatic на наличее ошибок

При срабатывании мониторига process_in_matchers_time_99_quant причина скорее всего в том что dispatcher не смог переподключится к матчерам. Можно просто порестартить диспатчеры

%%
for dc in {man,sas,vla}; do echo $dc; ya tools sedem p_exec  --dc $dc --cmd "yacare restart dispatcher" maps_core_jams_matcher_stable maps_core_jams_matcher_prestable; done
%%

## Documentation

(https://wiki.yandex-team.ru/users/kor-den/Matchingapi/)
(https://wiki.yandex-team.ru/users/kor-den/matchingexternalapi/)

## Known clients
- Yandex auto


## SLA

Будет после закрытия GEOINFRA-2038


## Persistent Volumes
* /persistent - основной раздел для хранения состояния, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/jams/matcher
* /graph - раздул для хранения верий графа, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic
  * /var/spool/yandex/maps/graph
  * /usr/share/yandex/maps
* /logs - логи, сюда ставится симлинка из /var/log



## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_JAMS_MATCHER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_MATCHER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_JAMS_MATCHER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_MATCHER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSNAVI?service=jams_matcher
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/24173
    * Тикет: https://lunapark.yandex-team.ru/MAPSNAVI-5055
