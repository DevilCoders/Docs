# Constructor

[![production version](https://badger.yandex-team.ru/qloud/maps/front-constructor/production/app/env-version.svg)](https://platform.yandex-team.ru/projects/maps/front-constructor/production) [![testing version](https://badger.yandex-team.ru/qloud/maps/front-constructor/testing/app/env-version.svg)](https://platform.yandex-team.ru/projects/maps/front-constructor/testing)

The Map Constructor is a visual map editor where you can create your own map with placemarks, lines, and polygons.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-constructor |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-constructor/ |
| AWACS | [front-constructor.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-constructor.slb.maps.yandex.net/show/) |
| Tanker | https://tanker.yandex-team.ru/?project=constructor3&branch=master |

## Instances

| Environment | URL |
|---|---|
| Testing | https://l7test.yandex.ru/map-constructor/ |
| Production | https://yandex.ru/map-constructor/ |

## Documentation

API method documentation and API enitities description can be found in [docs/spec.yaml](docs/spec.yaml)

## What happens when service is down

Constructor will stop working.

## Grants

### For blackbox
* https://grantushka.yandex-team.ru/grants/issue/19011/
* https://grantushka.yandex-team.ru/grants/issue/19017/
* https://grantushka.yandex-team.ru/grants/issue/19049/

**Attributes**
```javascript
"attributes": {
    "login": 1008,
    "fio": 1007,
    "sex": 29,
    "email": 14,
    "country": 31,
    "lang": 34
}
```

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-constructor_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-constructor_production |
| Balancer | [porto metrics](https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-constructor.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-constructor.slb.maps.yandex.net/), [requests](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-constructor.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-constructor.slb.maps.yandex.net/)

## Backend dashboards

| Name | URL |
|---|---|
| constructor-int | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-constructor-int.production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout`, `/run/qloud/app.stderr` |
| Nginx, DoBlu Agent, Juggler Client, Push client | `/var/log/supervisor/` |
| YT  | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "front-constructor_app"` |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
