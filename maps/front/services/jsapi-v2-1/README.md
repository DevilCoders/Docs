# `jsapi v2.1`
`Javascript Yandex Maps API`

## General information

| Key | Value |
|---|---|
| ABC | (deprecated) https://abc.yandex-team.ru/services/maps-front-jsapi-2_1 <br> (new) https://abc.yandex-team.ru/services/maps-front-jsapi-v2-1 |
| Deploy | https://yd.yandex-team.ru/projects/maps-front-jsapi-v2-1 |
| CI | - |
| Statistics | https://stat.yandex-team.ru/Api_Maps_Clean |
| Tanker | https://tanker-beta.yandex-team.ru/project/maps_api <br> (translate only RU EN TR UK, the rest are partially used in n.maps.yandex.ru) |
| TestPalm | https://testpalm2.yandex-team.ru/maps-js-api |

## Instances

| Environment | URL |
|---|---|
| Testing | https://api-maps.tst.c.maps.yandex.ru/2.1/ |
| Prestable | - |
| Production | https://api-maps.yandex.ru/2.1/ |

You can use 2.1 or 2.1.'minor version number' to get api. Read more about [api versioning](https://tech.yandex.com/maps/doc/jsapi/2.1/versions/concepts/index-docpage/).

## Documentation

See documentation in [our wiki](https://wiki.yandex-team.ru/maps/api).

Official [API documentation](https://tech.yandex.com/maps/doc/jsapi/2.1/quick-start/tasks/quick-start-docpage/).

Functional autotests [documentation](tests/hermione/README.md).

Functional manual tests [documentation](tests/manual/README.md).

## What happens when service is down
All services which show Yandex Maps via JS API will be affected (majority of the Runet sites).

Some of Yandex services will stop working:
* https://n.maps.yandex.ru/
* https://metro.yandex.ru/
* https://taxi.yandex.ru/
* Geo SERP wizards

or will work incorrectly in some cases:
* https://realty.yandex.ru/
* https://market.yandex.ru/
* https://afisha.yandex.ru/
* https://pogoda.yandex.ru/

and etc.

## How to fix common problems

### The timings of the Enterprise JS API are critically high
- The access to the enterprise JS API is restricted by the apikeys service. Usually if apikeys is failing it triggers degradation of JS API with it. So take a look at the [dashboard of apikeys](https://grafana.yandex-team.ru/d/6mcvzSNmk/maps-apikeys-back?orgId=1). If the "Error RPS" graph correlates to failing graphs in JS API, then contact someone from the [apikeys team](https://wiki.yandex-team.ru/maps/dev/ui/roles/#lichnyjjkabinet).

## SLA

* [JSAPI v2.1](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_jsapi_21) ([SLA config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/monitoring/tools/sla_calculator/core/services/maps_jsapi_21.py))
* [Enterprise JSAPI v2.1](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_jsapi_21_enterprise) ([SLA enterprise config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/monitoring/tools/sla_calculator/core/services/maps_jsapi_21_enterprise.py))

*Note*. Enterprise version upstream time is affected by upstream time of [apikeys service](https://wiki.yandex-team.ru/maps/dev/ui/libs/apikeys/).

## Monitorings
| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-jsapi-v2-1-*_production.app |

Configuration is in `.qtools.json`.

## Dashboards
| Name | URL |
|---|---|
| Golovan | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-jsapi-v2-1-78_production/ |
| yastatic | https://yasm.yandex-team.ru/template/panel/yastatic_pannel/uuid=yastatic_net_s3_expert_front-maps-static_front-maps-static |

## Logs
| Name | URL/path |
|---|---|
| NodeJS | `logs -std{out,err} -1000` <br> `/porto_log_files/app_workload_std{out,err}.portolog` |
| Deploy | https://yd.yandex-team.ru/stages/maps-front-jsapi-v2-1-78_production/logs |
| Nginx, DorBlu Agent, Juggler Client, Push client | /var/log/supervisor/ |
| YT | [hahn.`home/logfeller/logs/maps-front-production-log`](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log) `tskv_format = 'front-jsapi-v2-1_v2-1-74'` [yql example](https://yql.yandex-team.ru/Operations/XVvduglcTpHZhtk1kU99lL7K7zwfBeOhvXcgqpIeiJk=) |
| yastatic timings | https://yql.yandex-team.ru/Operations/Xxhd653udvLAZiiGwGKAo6GvsQHVOUxvIGCuv9JoJiA= |

## Statistics
* [Запросы к панорамам с бесплатного API](https://yql.yandex-team.ru/Operations/WNDn_VlxuGPf7T6ZJc9IcnymkGJPXZMf-iOpSVJLkLw=)
* [Запросы к панорамам с платного API (apikey)](https://yql.yandex-team.ru/Operations/WMLCq1lxuNjJqSQgc2mCq5INovDr229pVyL1DlDBlNM=)
* [Запросы к панорамам с конкретного домена (referer)](https://yql.yandex-team.ru/Operations/WQHN7-fTKfVCb7Kt6GuXajFetI172UZYbdJbYxVh8WE=)
* [Запросы с api-key по ip](https://yql.yandex-team.ru/Operations/WMvlbT1IP_ssasWEhkx4A0uNF2zb37cxZLf7rqRxJc8=)
* [Запросы через поиск на определенном домене](https://yql.yandex-team.ru/Operations/WMpHvefTKTn02uHl8f2NJcWbstal23SLlP6oxUcsISE=)
* [Запросы к бесплатному API с apikey](https://yql.yandex-team.ru/Operations/WKxhz1lxuLTvshKK99v1XrPuZwtX_7br_wHjdUtQlfY=)
* [Запросы к бесплатному API с referer](https://yql.yandex-team.ru/Operations/WPCz3-fTKc07uQtua3AIm5LoPpkm62Hig_D248s90hQ=)
* [Запросы к платному API c apikey](https://yql.yandex-team.ru/Operations/WKMflFlxuLTvse9q5WC0s2Gy9U-1LclQBSIb5V-J7Yg=)
* [Деньги и хиты в рекламу по логам Директа](https://yql.yandex-team.ru/Operations/WMan6llxuNjJqTEjLVVtE4zHvMtWSSZ9qbtCFSIkt4M=)

## Regression Stress Testing Configurations
Combine stress testing

| Type | URL |
|---|---|
| Capacity | - |
| Stability | - |

## Support

- [База знаний](https://maps-api.daas.yandex-team.ru/)
- [Сообщить об ошибке в Базе знаний](https://forms.yandex-team.ru/surveys/73993)
