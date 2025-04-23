# agent-proxy / signals-uploader

Получает сигналы, сделанные в мобильных приложениях:
- "Мобильная Народная карта";
- "Приватное приложение для объездов".

Выдает задания в "Приватном приложении для объездов".

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru), Михаил Плоткин (miplot@yandex-team.ru), Андрей Наплавков (naplavkov@yandex-team.ru) |
| Отвественные SRE | Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/agent-proxy |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-agent-proxy/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_AGENT_PROXY |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_agent_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_agent_proxy_stable/) | [ core-nmaps-mrc-agent-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-agent-proxy-stable-panel-main/) | [ maps_core_nmaps_mrc_agent_proxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_agent_proxy_stable) |
| Testing | [maps_core_nmaps_mrc_agent_proxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_agent_proxy_testing/) | [ core-nmaps-mrc-agent-proxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-agent-proxy-testing-panel-main/) | [ maps_core_nmaps_mrc_agent_proxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_agent_proxy_testing) |
[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-agent-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-agent-proxy)
[Ratelimiter panel](https://yasm.yandex-team.ru/template/panel/maps_core_nmaps_mrc_agent_proxy-ratelimiter2-panel)

| Staging | User panels |
| ------- | ----------- |
| Stable  | [dbaas_postgres_metrics](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=117eed12-3358-4c5e-b713-6cbf1d57e54e;dbname=maps_mrc) |
| Testing | [dbaas_postgres_metrics](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=dcddf4d9-6276-4f2a-9e11-3c07cab2ccd1;dbname=maps_mrc_testing) |
| Stable  | [mds-ns-space](https://yasm.yandex-team.ru/template/panel/mds-ns-space/prj=maps_mrc/?range=604800000)

### Balancers

| Staging | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | -------------- | -------------- | ----------------------- |
| Stable | [core-nmaps-mrc-agent-proxy.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-agent-proxy.maps.yandex.net/) | [core-nmaps-mrc-agent-proxy.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-nmaps-mrc-agent-proxy.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-nmaps-mrc-agent-proxy-maps;signal=service_total) | [rtc_balancer_core-nmaps-mrc-agent-proxy_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-agent-proxy_maps_yandex_net_man)<br>[rtc_balancer_core-nmaps-mrc-agent-proxy_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-agent-proxy_maps_yandex_net_sas)<br>[rtc_balancer_core-nmaps-mrc-agent-proxy_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-agent-proxy_maps_yandex_net_vla) |
| Testing | [core-nmaps-mrc-agent-proxy.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-nmaps-mrc-agent-proxy.common.testing.maps.yandex.net_default/show/) | [core-nmaps-mrc-agent-proxy.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=common.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=common.testing.maps.yandex.net;signal=core-nmaps-mrc-agent-proxy_common_testing_maps_yandex_net;) |  |

## What happens when service is down

В "Мобильной Народной карте" и "Приватном приложении для объездов" перестанет работать выгрузка данных.
Кроме того, в "Приватном приложении для объездов" перестанут выдаваться задания.

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/mrc-agent-proxy/* |
| Uploader service | /var/log/yandex/maps/mrc-signals-uploader/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`//home/logfeller/logs/maps-log/1d/2021-02-14` WHERE tskv_format='mrc-agent-proxy'```; |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

## Known clients

- "Мобильная Народная карта";
- "Приватное приложение для объездов".

## Ecstatic Datasets

| Stable | Testing |
| ------ | ------- |
| [yandex-maps-geodata6](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geodata6/versions) | [yandex-maps-geodata6](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata6/versions) |
| [yandex-maps-mrc-graph-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-graph-pro/versions) | [yandex-maps-mrc-graph-pro](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-graph-pro/versions) |

## SLA

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | k5mb6zhpdowagz37.sas.yp-c.yandex.net |
| Stable | gb32worncdscxp3k.man.yp-c.yandex.net |
| Stable | wh3fj23b2aezhnou.vla.yp-c.yandex.net |
| Testing | gdtaaevkl3ct7b3l.sas.yp-c.yandex.net |

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_MRC_AGENT_PROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_AGENT_PROXY_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_MRC_AGENT_PROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_AGENT_PROXY_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations

## Localization

Service use localization tokens from [tanker](https://tanker.yandex-team.ru/?project=maps_core_mrc&branch=master&keyset=agent-proxy).
