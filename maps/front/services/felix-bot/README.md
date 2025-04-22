# felix-bot

[![build status](https://badger.yandex-team.ru/github/maps/felix-bot/master/state.svg)](https://github.yandex-team.ru/maps/felix-bot/commits/master)
[![oko health](https://badger.yandex-team.ru/oko/repo/maps/felix-bot/health.svg)](https://oko.yandex-team.ru/repo/maps/felix-bot)

TBD

## General information

| Key | Value |
|---|---|
| ABC | [maps-front-felix-bot](https://abc.yandex-team.ru/services/maps-front-felix-bot/) |
| CI | [Trendbox CI](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&type=TRENDBOX_CI_BUILD_BETA&desc_re=maps%5C%2Ffelix-bot&created=7_days&forPage=tasks) |
| Deploy | [maps-front-felix-bot](https://deploy.yandex-team.ru/projects/maps-front-felix-bot) |

## Instances

| Environment | URL | Secrets |
|---|---|---|
| Production | `felix-bot.maps.yandex.net` | [yav](https://yav.yandex-team.ru/secret/sec-01epy5kw0s9bazxftd30dxngx4/explore/versions) |

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory.

## Known clients

* Telegram
* Slack (for mobile team)
* Q

## What happens when service is down

TBA

## How to fix common problems

Try to restart application:

```sh
supervisorctl restart node
```

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/?query=host%3Dmaps-front-felix-bot_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | [maps.front-felix-bot.production](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-felix-bot_production) |
| DB | TBA |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/porto_log_files/app_workload_stdout.portolog`, `/porto_log_files/app_workload_stderr.portolog` |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |

## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Graphics | TBA |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
