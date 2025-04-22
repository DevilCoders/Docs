# Фронтенд сервиса Яндекс Go

[wiki](https://wiki.yandex-team.ru/taxi/frontend/go-constructor/)

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354856/info)

* NGINX - [taxifrontend-taxi-frontend-go](/services/taxifrontend-taxi-frontend-go/etc/nginx/sites-available/taxifrontend-taxi-frontend-go.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка и разработка

- `cd services/taxifrontend-taxi-frontend-go/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
