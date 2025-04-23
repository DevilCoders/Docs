# `GeoXML Service`

![production version](https://badger.yandex-team.ru/github/maps/geoxml-service/master/state.svg)

Geoxml caching & sanitizing proxy for Yandex.Maps API

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-geoxml-service/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-geoxml-service |
| Source name | geoxml_service |

## Instances

| Environment | URL |
|---|---|
| Testing | https://api-maps.tst.c.maps.yandex.ru/services/geoxml/1.2/geoxml.xml |
| Production | https://api-maps.yandex.ru/services/geoxml/1.2/geoxml.xml |

### Examples
```
https://api-maps.tst.c.maps.yandex.ru/services/geoxml/1.2/geoxml.xml?callback=id_154297680975131614884&url=https%3A%2F%2Fsandbox.api.maps.yandex.net%2Fexamples%2Fru%2F2.1%2Fymapsml_ballooncontentstyle%2Fdata.xml
```

## Known clients
It's a public API. It uses by a lot of external clients.

## What happens when service is down

Thousands of external sites stop working or work incorrectly. That means a lot of complaints to our support team.

## How to fix common problems

Restart service

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-geoxml-service_production.app |
| YASM | https://yasm.yandex-team.ru/template/alert/maps-front-geoxml-service-production-app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-geoxml-service_production |
| GoZora Client Health | https://solomon.yandex-team.ru/?project=zora&cluster=production&host=cluster&dashboard=gozora-client-health&client=geoxml_service |

## Logs

| Name | URL/path |
|---|---|
| Deploy | https://deploy.yandex-team.ru/stage/maps-front-geoxml-service_production/logs |
| Nginx, DoBlu Agent, Juggler Client, Push client | `/var/log/supervisor/` |
| YT  | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-geoxml-service_app"` |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
