# Графики и мониторинги

Страница SEDEM со сводной информацией про сервер Огорода: [ссылка](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs={%22sedem_service%22:%20%22core-garden-server%22})

## Джагглер

Мониторинги сервера Огорода: [ссылка](https://juggler.yandex-team.ru/dashboards/maps_core_garden_server)

Мониторинги модулей: [ссылка](https://juggler.yandex-team.ru/dashboards/maps_core_garden_modules)

Мониторинги квоты в YT: [ссылка](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dyt_quota_usage%20%26%20(tag%3Dgarden%20%7C%20tag%3Dgarden-exp))

Для ряда мониторингов вручную были настроены нотификации:
* YT -> Startrek [ссылка](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5e4d38522c7c4400724ec409)
* YT -> Telegram [ссылка](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5d481a09dcc66c006b26817a)

## Голован

Состояние сервера: [ссылка](https://yasm.yandex-team.ru/panel/robot-garden.maps-garden-manager-2/)

Текущие запущенные модули: [ссылка](https://yasm.yandex-team.ru/template/panel/maps-garden-manager-builds-metrics)

## Статистика

Работа модулей в YT: [ссылка](https://dash.yandex-team.ru/rlc80mom129go)

Релизный процесс: [ссылка](https://charts.yandex-team.ru/preview/nb1eyaujmiacm?env=production)

## SLA

Документация: [ссылка](https://wiki.yandex-team.ru/geo-infra/how-to/sla/)

Тайминги: [ссылка](https://datalens.yandex-team.ru/preview/c7e74d9fw4ce5-maps-sla-charts?impact_type=timings&title=maps_core_garden_server)

Коды ошибок: [ссылка](https://datalens.yandex-team.ru/preview/c7e74d9fw4ce5-maps-sla-charts?impact_type=codes&title=maps_core_garden_server)
