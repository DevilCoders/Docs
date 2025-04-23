# Сервис для получения, обогащения и хранения звонков по объявлениям

## Назначение

Колтрекинг Авто.ру - система, предназначенная для хранения и систематизации фактов звонков пользователей и дилеров в контексте сервиса Авто.ру.

Бизнес-задача: https://nda.ya.ru/t/vknlDQVR3VxDpr

## Модули
- api –– API сервиса
- scheduler –– модуль, отвечающий за сбор, обогащение и хранение данных о звонках

## Тимсити
[api](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_calltracking_api_release)

[scheduler](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_calltracking_scheduler_release)

## Логи
[api](https://nda.ya.ru/t/uG-IELOy3VxDrr)

[scheduler](https://nda.ya.ru/t/SvIeaGPO3VxDs9)

## Метрики
[gRPC сервер](https://nda.ya.ru/t/wprmDufW3VxEfA)

[gRPC клиент api-server](https://nda.ya.ru/t/nKFsdm5-3VxDqm)

[Консъюмеры](https://nda.ya.ru/t/Im-ROQqW3VxDq7)

## Sentry
[api](https://sentry.vertis.yandex.net/verticals/callracking-api/)

[scheduler](https://sentry.vertis.yandex.net/verticals/callracking-scheduler/)

## Jaeger
[api](https://nda.ya.ru/t/iKeotg6m3VxDrU)

## Интеграции и процесс
#### _кликабельно, внутри ссылки на код_
[<img src="docs/autoru-calltracking.svg">](docs/autoru-calltracking.svg)
[Исходник схемы для редактирования в drawio.yandex-team.ru](docs/autoru-calltracking.drawio)

