# Фронтенд сервиса Divkit render

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [eda-divkit-render](/services/eda-divkit-render/etc/nginx/sites-available/eda-divkit-render.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка и разработка

- `cd services/eda-divkit-render/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
