# Tracker for map editor
Frontend of tracker for public map editor.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-nmaps |
| Statistics | https://metrika.yandex.ru/dashboard?id=36706330 |
| Tanker | https://tanker.yandex-team.ru/?project=nmaps-tracker |

## Instances

| Environment | URL |
|---|---|
| Testing | https://nmaps.tst.maps.yandex.ru/tracker |
| Production | https://n.maps.yandex.ru/tracker <br/> https://mapeditor.yandex.com/tracker |

## Debian dependencies

  * [uatraits-data](https://c.yandex-team.ru/packages/uatraits-data)
  * [uatraits-nodejs](https://c.yandex-team.ru/packages/uatraits-nodejs)

## What happens when service is down

Users aren't able to add points and tracks.

## SLA
99.9% requests are handled properly.
* HTTP code of the response is not 5xx.
* Upstream time is less than 500 ms on the 98th percentile.

## Monitorings

### production

## Dashboards
| Name | URL |
|---|---|
| Alerts | [JUGGLER](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-nmaps-tracker_production.app) |
| Main | [YASM](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-nmaps-tracker_production) |

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/access.log, /var/log/nginx/error.log |
| Deploy | https://deploy.yandex-team.ru/stage/maps-front-nmaps-tracker_production/logs |
| YT | [hahn.[home/logfeller/logs/maps-front-production-log/1d]](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log) `tskv_format = 'front-nmaps-tracker_app'` [YQL](https://yql.yandex-team.ru/Operations/XTYFUWHljruLH_8VtmHVv_WyzH_LHtrbEwC_zHxX8yA=) |

## Developing

### Getting started

TODO

## Wiki
See https://wiki.yandex-team.ru/maps/dev/ui/products/nmaps-tracker/ for some details
