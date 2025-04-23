# Фронтенд сервиса Сервис для приложения получателя Чаевых

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [eda-front-eats-tips-app](/services/eda-front-eats-tips-app/etc/nginx/sites-available/eda-front-eats-tips-app.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

- `cd services/eda-front-eats-tips-app/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
