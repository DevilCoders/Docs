# `maps-telegram-bot`

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-telegram-bot/ |
| Qloud | https://platform.yandex-team.ru/projects/maps/front-telegram-bot |
| Tanker | https://tanker.yandex-team.ru/?project=yandex-maps-telegram-bot |

## Secrets

 Environment | URL |
|---|---|
| production | https://yav.yandex-team.ru/secret/sec-01crb5dj8tx09fcy9hdjahwetp |
| development | https://yav.yandex-team.ru/secret/sec-01crb53pt63jy8gfcpnq1mcw9r |

## Instances

| Environment | URL |
|---|---|
| Production | https://telegram-bot.maps.yandex.net/ |

## What happens when service is down

Telegram bot [@YandexMapsBot](https://telegram.me/@YandexMapsBot) stops working.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-telegram-bot_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-telegram-bot_production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `logs stdout`, `/logs stderr` |
| Supervisor | `/var/log/supervisor/` |
| YT  | hahn.`home/logfeller/logs/maps-front-production-log` [yql example](https://yql.yandex-team.ru/Operations/XRsMZmHljo954m9DuWOw9hzN4mhszd-urV67L7Z_20A=) |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
