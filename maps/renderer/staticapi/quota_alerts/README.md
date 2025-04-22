# Шаблоны алертов по квотам клиентов API

| Шаблон в Головане | Проверки в Juggler | Описание |
| ----------------- | ------------------ | -------- |
| [maps_core_renderer_staticapi_quota_stable](https://yasm.yandex-team.ru/template/alert/maps_core_renderer_staticapi_quota_stable) | [maps_core_renderer_staticapi_quota_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_quota_stable&view=tiles&limit=200) | алерты по квотам в stable |
| [maps_core_renderer_staticapi_quota_testing](https://yasm.yandex-team.ru/template/alert/maps_core_renderer_staticapi_quota_testing) | [maps_core_renderer_staticapi_quota_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_quota_testing&view=tiles&limit=200) | алерты по квотам в testing |
| [maps_core_renderer_staticapi_quota_common](https://yasm.yandex-team.ru/template/alert/maps_core_renderer_staticapi_quota_common) | | вспомогательные функции |

Графики и сигналы: [maps_core_renderer_staticapi-ratelimiter2-panel](https://yasm.yandex-team.ru/template/panel/maps_core_renderer_staticapi-ratelimiter2-panel)

Документация про квоты: https://docs.yandex-team.ru/static-maps/quotas

## Как обновлять шаблоны алертов

1. Обновить шаблон: `curl --data-binary @<template_name>.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=<template_name>'`
2. Сгенерировать алерты: `curl -XPOST 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/<template_name>'`

Подробнее в документации Голована:
- [API шаблонов алертов](https://wiki.yandex-team.ru/golovan/userdocs/templatium/alerts/api/)
- [Работа с шаблонами алертов в UI](https://wiki.yandex-team.ru/golovan/userdocs/templatium/alerts/ui/)
