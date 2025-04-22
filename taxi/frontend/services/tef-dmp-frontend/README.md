# Фронтенд сервиса Просмотр текущего состояния процессов DMP и метаинформации по данным

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [tef-dmp-frontend](/services/tef-dmp-frontend/etc/nginx/sites-available/tef-dmp-frontend.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

- `cd services/tef-dmp-frontend/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
