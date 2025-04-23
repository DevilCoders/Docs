# Фронтенд сервиса Yango

[wiki](https://wiki.yandex-team.ru/taxi/frontend/yango-site/)

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354855/info)

* NGINX - [taxifrontend-taxi-frontend-yango](/services/taxifrontend-taxi-frontend-yango/etc/nginx/sites-available/taxifrontend-taxi-frontend-yango.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка и разработка

- `cd services/taxifrontend-taxi-frontend-yango/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
