# Garden
Backoffice for building geodata

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-garden |
| Product manager | https://staff.yandex-team.ru/tail |
| Backend | https://staff.yandex-team.ru/alexbobkov |
| Frontend | https://staff.yandex-team.ru/smith, <br/> https://staff.yandex-team.ru/makishvili |
| SRE | https://staff.yandex-team.ru/morbid |
| Fuckups chat | https://t.me/joinchat/BEZLV0M4Cg64KSsBy5lv7Q |
| Tracker Queue | https://st.yandex-team.ru/MAPSGARDEN |
| Repository | https://a.yandex-team.ru/arc_vcs/maps/front/services/garden |


## Instances

| Environment | URL |
|---|---|
| Testing | https://garden.tst.c.maps.yandex-team.ru/ |
| Production | https://garden.maps.yandex-team.ru |

## What happens when service is down

Yandex cannot get new geodata.

## Monitorings

### production
| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-garden_production.app |
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-garden-production-app |

## Dashboards
| Name | URL |
|---|---|
| Frontend (tst) | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-garden_testing |
| Frontend | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-garden_production |
| Backend | https://yasm.yandex-team.ru/panel/robot-garden.maps-garden-manager-2 |

## Logs
| Name | URL/path |
|---|---|
| Nginx, Juggler Client, Push client | `/var/log/supervisor` |
| YT | [//home/logfeller/logs/maps-front-production-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log) |

----

## Documentation and Developing

* [How to start](CONTRIBUTING.md)
* [How to deploy](docs/deploy.md)
