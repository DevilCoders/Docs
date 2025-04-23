# Yandex Maps

[![](https://badger.yandex-team.ru/custom/[Stand]/[trunk][blue]/badge.svg)](https://maps-trunk.stands.maps.yandex.ru/maps/)
[![](https://badger.yandex-team.ru/custom/[Storybook]/[trunk][blue]/badge.svg)](https://podrick.c.maps.yandex-team.ru/report-proxy/sandbox/owner=MAPS_FRONT&type=TRENDBOX_CI_REPORT_RESOURCE_BETA&project=maps-front-maps&branch=trunk&step=STORYBOOK/)
[![](https://badger.yandex-team.ru/custom/[Testcop]/[trunk][yellow]/badge.svg)](https://testcop.si.yandex-team.ru/skips/hermione/maps)

## General information

| Key                 | Value                                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------------------------ |
| ABC                 | https://abc.yandex-team.ru/services/maps-front-maps                                                    |
| CI                  | [Trendbox UI](https://trendbox-ui.s3.mds.yandex.net/latest/index.html?text=repository:arc:maps/front#/) |
| Deploy              | https://deploy.yandex-team.ru/projects/maps-front-maps                                                 |
| [RPS Limiter](#rps-limiter) |                          |
| Antirobot           | https://cbb-ext.yandex-team.ru/tag/cbbmaps                                                             |
| Statistics          | https://datalens.yandex-team.ru/tuod7x0dyej2p-1-webandtouchmapskpidashboard                            |
| Tanker              | https://tanker-beta.yandex-team.ru/project/loris?branch=master                                         |
| Bunker              | https://bunker.yandex-team.ru/maps-www/                                                                |
| Sender (testing)    | https://test.sender.yandex-team.ru/maps/campaign/                                                      |
| Sender (production) | https://sender.yandex-team.ru/maps/campaign/                                                           |

## How to fix fuckups?

Read [here](./docs/incident.md).

## Instances

| Environment                      | URL                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Testing                          | https://l7test.yandex.ru/maps/, <br>https://l7test.yandex.ru/metro/                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Testing (production environment) | https://maps-rc.l7test.yandex.ru/maps/                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Production                       | https://yandex.ru/maps/, <br>https://yandex.ru/harita/, <br>https://yandex.ru/web-maps/, <br>https://yandex.ru/navi/, <br>https://yandex.ru/metro/, <br><details><summary>Other domains</summary>https://yandex.az/maps/, <br>https://yandex.by/maps/, <br>https://yandex.co.il/maps/, <br>https://yandex.com/maps/, <br>https://yandex.com.am/maps/, <br>https://yandex.com.ge/maps/, <br>https://yandex.com.tr/harita/, <br>https://yandex.ee/maps/, <br>https://yandex.eu/maps/, <br>https://yandex.fi/maps/, <br>https://yandex.fr/maps/, <br>https://yandex.kg/maps/, <br>https://yandex.kz/maps/, <br>https://yandex.lt/maps/, <br>https://yandex.lv/maps/, <br>https://yandex.md/maps/, <br>https://yandex.pl/maps/, <br>https://yandex.tj/maps/, <br>https://yandex.tm/maps/, <br>https://yandex.ua/maps/, <br>https://yandex.uz/maps/</detailts> |

### L7 balancers

| Environment | Namespace                                                                                                                              | Requests Stats                                                                                                                                                                                                                | Instance Stats                                                                                                                                                                                                   |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Testing     | [front-maps.tst.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps.tst.slb.maps.yandex.net/show/) | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-maps.tst.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-maps.tst.slb.maps.yandex.net;signal=mapstest;) | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-maps.tst.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-maps.tst.slb.maps.yandex.net;) |
| Production  | [front-maps.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps.slb.maps.yandex.net/show/)         | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-maps.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-maps.slb.maps.yandex.net;signal=maps;)             | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-maps.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-maps.slb.maps.yandex.net;)         |

[Detailed scheme](./docs/balancing-scheme.md) of the balancering.

## Secrets

| Name                             | Link                                                             |
| -------------------------------- | ---------------------------------------------------------------- |
| maps-front-maps.production       | https://yav.yandex-team.ru/secret/sec-01ckzrndkkqg2egcr8kdqysqh3 |
| maps-front-maps.testing          | https://yav.yandex-team.ru/secret/sec-01ckzexfhcp5tv3pjxhgj2217b |
| maps-front-maps-external-account | https://yav.yandex-team.ru/secret/sec-01f9ejjx2mp6w9ez429v670hwp |

## RPS Limiter

| Service | Link |
| --- | --- |
| maps | https://rpslimiter.z.yandex-team.ru/records/maps_front/front-maps/editor |
| metro | https://rpslimiter.z.yandex-team.ru/records/maps_front/front-metro/editor |
| map-widget | https://rpslimiter.z.yandex-team.ru/records/maps_front/front-map-frame-api/editor |

## Documentation

Glossary: https://wiki.yandex-team.ru/maps/docs/

https://wiki.yandex-team.ru/maps/dev/ui/products/maps/

## SLA

99.9% requests are handled properly.

-   HTTP code of the response is not 5xx.
-   Upstream time is less than 500 ms on the 98th percentile.

## Monitorings

### production

| Type    | URL                                                                                                                            |
| ------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Juggler | [maps-front-maps_production.maps](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-maps_production.maps) |
| Golovan | [maps-front-maps-production-maps](https://yasm.yandex-team.ru/template/alert/maps-front-maps-production-maps)                    |

### metro production

| Type    | URL                                                                                                                                |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Juggler | [maps-front-maps_production.metro](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-maps_production.metro) |
| Golovan | [maps-front-maps-production-metro](https://yasm.yandex-team.ru/template/alert/maps-front-maps-production-metro/)                   |

### map-widget production

| Type    | URL                                                                                                                                          |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Juggler | [maps-front-maps_production.map-widget](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-maps_production.map-widget) |
| Golovan | [maps-front-maps-production-map-widget](https://yasm.yandex-team.ru/template/alert/maps-front-maps-production-map-widget)                    |

## Dashboards

| Name          | URL                                                                                                                                                                               |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Main          | [Panel `front-maps`](https://yasm.yandex-team.ru/panel/front-maps?range=7200000)                                                                                                  |
| Autogenerated | [Common panel `maps-front-maps_production`](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-maps_production;unit=maps;workload=maps_workload/?range=7200000)       |
| RUM           | [rum.yandex-team.ru](https://rum.yandex-team.ru/projects/maps)                                                                                                                    |
| Client errors | [error.yandex-team.ru](https://error.yandex-team.ru/projects/maps)                                                                                                                |
| Client events | [events.chv.yandex-team.ru](https://events.chv.yandex-team.ru/projects/maps)                                                                                                      |
| CSP errors    | [csp.yandex-team.ru](https://csp.yandex-team.ru/projects/maps/projectDashboard)                                                                                                   |
| L7 balancer   | [Panel `l7_balancer_weighted_service_requests`](https://yasm.yandex-team.ru/template/panel/l7_balancer_weighted_service_requests/prj=l7-balancer-term;signal=maps/?range=7200000) |
| Antirobot | [Panel `antirobot_for_service`](https://yasm.yandex-team.ru/template/panel/antirobot_for_service/service=maps/) |

## Logs

| Name          | path                                            | URL                                                                                                                                                                | Example                                                                                   |
| ------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------- |
| NodeJS stderr | `/porto_log_files/app_workload_stderr.portolog` |                                                                                                                                                                    |                                                                                           |
| NodeJS stdout | `/porto_log_files/app_workload_stdout.portolog` | [arnold.[logs/deploy-logs/1d]](https://yt.yandex-team.ru/arnold/#page=navigation&path=//logs/deploy-logs/1d)                                                       | [YQL](https://yql.yandex-team.ru/Operations/YfP_aK5ODzHFlKe07Hb9R78jOE6YBQL1VDFun95Mex4=) |
| Nginx errors  | `/var/log/nginx/error.log`                      |                                                                                                                                                                    |                                                                                           |
| Nginx access  | `/var/log/nginx/access.log`                     | [hahn.[home/logfeller/logs/maps-front-production-log/1d]](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/logfeller/logs/maps-front-production-log/1d) | [YQL](https://yql.yandex-team.ru/Operations/YfQEG5fFt8LH3YAiWk6gKJvekREURlwEQb3SpdVYAU4=) |
| L7 access     |                                                 | [hahn.[home/logfeller/logs/l7-balancer-access-log/1d]](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/l7-balancer-access-log/1d)             | [YQL](https://yql.yandex-team.ru/Operations/XXi49VPzVLAle2gZTR6YJQktKfAPdXtxDyIrxpJF8Rs=) |

## Regression Stress Testing Configurations

[Capacity + Stability](https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=maps-front-maps)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
