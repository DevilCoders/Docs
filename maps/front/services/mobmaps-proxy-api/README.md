# mobmaps-proxy
Proxy to internal services used by Geo mobile applications.

All frontend services add their own end-points which proxy all requests to the internal http services. It makes it possible to add some extra work before request is sent. For example, checking a request signature as it is done in `yandex.tls/maps/api/`.

Mobile applications use Mapkit end-points to obtain data. However, sometimes mobile application needs an extra data which it cannot get from Mapkit. All parthners data providers are put to `mobmaps-proxy`.

Or sometimes it is not possible to use Mapkit at all. For instance, Yandex Maps Widget for Android uses router but widget must be lightweight; so, it uses `mobmaps-proxy` to get time and distance from router backend.

You can get oauth token via [test application](https://oauth.yandex.ru/authorize?response_type=token&client_id=c30de138ea5b41cb8a6352a2617531b7);

## General Information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-mobmaps-proxy-api |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-mobmaps-proxy-api |

## Instances

| Environment | Balancer host |
|---|---|
| Testing | https://mobmaps-proxy-api.tst.c.maps.yandex.net/ |
| External testing | https://mobmaps-proxy-api-ext.c.maps.yandex.net/ |
| Production | https://geointernal.mob.maps.yandex.net/ |

`Testing` is a special server which is available from the Internet. See [MAPADMIN-26611](https://st.yandex-team.ru/MAPADMIN-26611#1489659346000).

## API Documentation
API method documentation in [swagger](http://swagger.io/specification/) format can be found in [docs](docs) directory.

## Known clients

* Yandex Maps App
* Yandex Transport App
* Yandex Metro App

## What happens when service is down

Part of mobile applications will work incorrectly. For example, Yandex Maps App cannot open seo urls or send feedback for businesses.

## How to fix common problems
### Restart service
```
# supervisorctl restart node
```

### Change log level
0. ssh to the desired instance.
1. Open the config file `vim /usr/local/app/configs/production.yaml`.
2. Find the `logger` section.
3. Change the `level` property to one for the [supported ones](https://github.com/winstonjs/winston#logging-levels).
4. Restart the service.

**Note.** Do not forget to change the log level to the previous value, when you've finished debugging.

## Grants
Blackbox: https://grantushka.yandex-team.ru/grants/issue/20965/

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-mobmaps-proxy-api_production.app |

## Dashboards

| Name | URL |
|---|---|
| Production | [Golovan](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-mobmaps-proxy-api_production;mode=full) |
| Production (errors only) | [Golovan](https://yasm.yandex-team.ru/panel/_AnNz2C) |
| Testing | [Golovan](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-mobmaps-proxy-api_testing) |
| External-Testing | [Golovan](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-mobmaps-proxy-api_external-testing) |

## Backend dashboards

| Name | URL |
|---|---|
| userAccountInt | <https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-user-account-int.production/> |
| search | <https://yasm.yandex-team.ru/template/panel/addrs_kpi> |
| ugcSearch | <https://yasm.yandex-team.ru/template/panel/ugcserver_requests/> |
| discoveryInt | <https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-discovery-int.production> |
| masstransit | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-router-stable-panel-main/> |
| mtinfo | <https://yasm.yandex-team.ru/template/panel/maps-core-masstransit-mtinfo-stable-panel-main/> |
| router | <https://yasm.yandex-team.ru/template/panel/maps-core-driving-router-stable-panel-main/> |
| moiraInt | <https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-moira-int.production> |
| feedbackInt | <https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-feedback-int.production> |

## Logs

| Name | path | URL | Example |
|---|---|---|---|
| NodeJS stderr | `/porto_log_files/app_workload_stderr.portolog` | | |
| NodeJS stdout | `/porto_log_files/app_workload_stdout.portolog` | [arnold.[logs/deploy-logs/1d]](https://yt.yandex-team.ru/arnold/#page=navigation&path=//logs/deploy-logs/1d) | [YQL](https://yql.yandex-team.ru/Operations/X75cPhpqvzsWiNaAPerMcalxye-9a1OPx0zKy2uIOsg=) |
| Nginx errors | `/var/log/nginx/error.log` | | |
| Nginx access | `/var/log/nginx/access.log` | [hahn.[home/logfeller/logs/maps-front-production-log/1d]](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/logfeller/logs/maps-front-production-log/1d) | [YQL](https://yql.yandex-team.ru/Operations/X83tF2im9fe3Ugx562O15hlp0AiTYBpHLAnLS3hzz88=) |
| Nginx, Juggler Client, Push client | /var/log/supervisor/ | | |

## Regression Stress Testing Configurations

**TBA**

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
