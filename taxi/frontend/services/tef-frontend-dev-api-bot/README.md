# Фронтенд сервиса Бот автоматизации монорепы

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [frontend-dev-api-bot](/services/frontend-dev-api-bot/etc/nginx/sites-available/frontend-dev-api-bot.conf)
* unstable - [TODO](host)
* testing - [frontend-dev-api-bot.taxi.tst.yandex.net](http://frontend-dev-api-bot.taxi.tst.yandex.net)
* stable - [frontend-dev-api-bot.taxi.yandex.net](http://frontend-dev-api-bot.taxi.yandex.net)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка и разработка

- `cd services/frontend-dev-api-bot/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Логи

* Testing - https://kibana.taxi.tst.yandex-team.ru/goto/e680365248c2868c9c65cbd6fde27611
* Prod - https://kibana.taxi.yandex-team.ru/goto/4b9ec5101d4192c15821d6f79a7c7fa0
