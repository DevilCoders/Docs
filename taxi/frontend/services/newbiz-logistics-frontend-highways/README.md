# Фронтенд сервиса Сервис "Магистрали" для фронтенда Доставки

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [newbiz-logistics-frontend-highways](/services/newbiz-logistics-frontend-highways/etc/nginx/sites-available/newbiz-logistics-frontend-highways.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

- `cd services/newbiz-logistics-frontend-highways/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
