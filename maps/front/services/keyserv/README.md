# keyserv

Admin panel for Yandex Maps API users management. It consist of two parts: keys management and blocking violators who doesn't follow Yandex Maps API User agreement. It's possible to block violators by IP address, referrer or mobile application ID. Please note that for cyrillic referrers blocking you need to convert referrer to punycode.

See also:

* [Functional specification](https://wiki.yandex-team.ru/maps/data/navteq/design/)
* [Backend API documentation](https://wiki.yandex-team.ru/maps/dev/core/keyserv2/)

## General Information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-keyserv/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-keyserv |

## Instances

| Environment | URL |
|---|---|
| Testing | https://keyserv.tst.c.maps.yandex-team.ru/ |
| Production | https://keyserv.maps.yandex-team.ru/ |

## Grants

* Blackbox Internal for MAPSTESTQNETS:
    * https://grantushka.yandex-team.ru/grants/issue/22613/
    * https://grantushka.yandex-team.ru/grants/issue/22619/
    * https://grantushka.yandex-team.ru/grants/issue/22617/
    * https://grantushka.yandex-team.ru/grants/issue/27421/
    * https://grantushka.yandex-team.ru/grants/issue/27423/
* Blackbox Mimino for MAPSTESTQNETS:
    * https://grantushka.yandex-team.ru/grants/issue/22581/
    * https://grantushka.yandex-team.ru/grants/issue/22579/
* Blackbox Production for MAPSPRODQNETS:
    * https://grantushka.yandex-team.ru/grants/issue/22581/
    * https://grantushka.yandex-team.ru/grants/issue/22611/
    * https://grantushka.yandex-team.ru/grants/issue/27697/

## What happens when service is down

Part of mobile applications will work incorrectly. For example, Yandex Maps App cannot open seo urls or send feedback for businesses.

## How to fix common problems
### Restart service
```
# supervisorctl restart app
```

## Monitorings

| Type | URL |
|---|---|
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-keyserv-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-keyserv_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-keyserv_production  |

## Balancer

| Name | URL |
|---|---|
| Porto metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-keyserv.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-keyserv.slb.maps.yandex.net/ |
| Requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-keyserv.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-keyserv.slb.maps.yandex.net/ |

## Logs

| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stages/maps-front-keyserv_production/logs |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT | ``hahn.`home/logfeller/logs/maps-front-production-log/1d` ``, `tskv_format = "maps-front-keyserv_app"` |

## How to get access to the keyserv

Access is stricted by ABC services [maps-front-keyserv](https://abc.yandex-team.ru/services/maps-front-keyserv/) and [maps-front-keyserv-users](https://abc.yandex-team.ru/services/maps-front-keyserv-users/) — [related rule](https://puncher.yandex-team.ru/?id=6012e47211fb9e50a35323c6).
For getting access please add yourself to one of these ABC services.

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
