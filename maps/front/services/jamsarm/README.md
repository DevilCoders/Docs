# JAMS AWP2
Frontend of road events editor

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-jamsarm/|
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-jamsarm |

## Instances

| Environment | URL |
|---|---|
| Testing | https://jamsarm.tst.c.maps.yandex.ru |
| Production | https://points.maps.yandex.ru |

## What happens when service is down

Users cannot edit road events, view realtime tracks and manage access to the system

## Monitorings

### production

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-jamsarm_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-jamsarm_production |

## Logs

| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stage/maps-front-jamsarm_production/logs |
| Nginx | /var/log/nginx/access.log, /var/log/nginx/error.log |
| YT | [//home/logfeller/logs/maps-front-production-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log) `tskv_format = 'front-jams-awp2_app'` |

## Regression Stress Testing

| Name | URL |
|---|---|
| Startrek | https://st.yandex-team.ru/MAPSLOADTESTING-54 |
| Lunapark | https://lunapark.yandex-team.ru/MAPSLOADTESTING-54 |
| Capacity & Stability | https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING?service=front-jams-awp2 |
