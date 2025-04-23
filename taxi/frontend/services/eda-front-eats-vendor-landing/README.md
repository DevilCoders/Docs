# Фронтенд сервиса Партнерский лендинг для Вендорки

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [eda-front-eats-vendor-landing](/services/eda-front-eats-vendor-landing/etc/nginx/sites-available/eda-front-eats-vendor-landing.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* production - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

- `cd services/eda-front-eats-vendor-landing/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: production | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
