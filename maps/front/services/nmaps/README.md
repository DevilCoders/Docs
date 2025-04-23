# Map editor [![Oko health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=maps/front/services/nmaps)](https://oko.yandex-team.ru/arc/maps/front/services/nmaps)
Frontend of public map editor.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-nmaps |
| Statistics | https://stat.yandex-team.ru/Maps.Wiki<br/>https://stat.yandex-team.ru/Dashboard/Nmaps |
| Tanker | https://tanker-beta.yandex-team.ru/project/nmaps |

## Instances

| Environment | URL |
|---|---|
| Development | https://nmaps-trunk.stands.maps.yandex.ru |
| Testing | https://nmaps.tst.maps.yandex.ru<br/>https://nmaps.tst.maps.yandex.com<br/>https://nmaps.tst.maps.yandex.com.tr<br/>https://design-nmaps.tst.maps.yandex.ru<br/>https://npro.tst.c.maps.yandex.ru<br/>https://npro.tst.c.maps.yandex.com<br/>https://npro.tst.c.maps.yandex.com.tr |
| Crowd testing | https://front-nmaps.crowdtest.maps.yandex.ru<br/>https://front-npro.crowdtest.maps.yandex.ru |
| Mrc testing | https://nmaps-mrc-testing.tst.c.maps.yandex.ru<br/>https://nmaps-mrc-pro-testing.tst.c.maps.yandex.ru<br/>https://nmaps-mrc-pro-datatesting.tst.c.maps.yandex.ru<br/> |
| Production | https://n.maps.yandex.ru<br/>https://mapeditor.yandex.com<br/>https://mapeditor.yandex.com.tr<br/>https://npro.maps.yandex.ru |

## What happens when service is down

Users aren't able to edit map.

## SLA
99.9% requests are handled properly.
* HTTP code of the response is not 5xx.
* Upstream time is less than 500 ms on the 98th percentile.

## Monitorings

### production
| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-nmaps_production.app |
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-nmaps-production-app |

## Dashboards
| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-nmaps_production |
| Client errors | https://error.yandex-team.ru/projects/nmaps/ |

## Backend dashboards
| Name | URL |
|---|---|
| Wiki | https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/grafana-dashboards/ |

## Balancers
| Host | Namespace | Upstream |
|---|---|---|
| nmaps | [front-nmaps.slb.maps.yandex.net](https://deploy.yandex-team.ru/balancers/front-nmaps.slb.maps.yandex.net) | [main](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-nmaps.slb.maps.yandex.net/upstreams/list/main/show/) |
| npro | [front-npro.slb.maps.yandex.net](https://deploy.yandex-team.ru/balancers/front-npro.slb.maps.yandex.net) | [main](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-npro.slb.maps.yandex.net/upstreams/list/main/show/) |
| nmaps.tst | [front-testing.slb.maps.yandex.net](https://deploy.yandex-team.ru/balancers/front-testing.slb.maps.yandex.net) | [maps-front-nmaps](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/upstreams/list/maps-front-nmaps/show/) |

## Logs
| Name | URL/path |
|---|---|
| Deploy | https://deploy.yandex-team.ru/stage/maps-front-nmaps_production/logs |
| Nginx, Juggler Client, Push client | /var/log/supervisor/ |
| YT | [//home/logfeller/logs/maps-front-production-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log) `tskv_format = 'maps-front-nmaps_app'` |

## Regression Stress Testing Configurations
| Name | URL |
|---|---|
|Capacity|https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-nmaps|

How to make ammo files: https://wiki.yandex-team.ru/maps/dev/ui/tests/load/ammo-grep/

## Developing

[How to develop](CONTRIBUTING.md)
