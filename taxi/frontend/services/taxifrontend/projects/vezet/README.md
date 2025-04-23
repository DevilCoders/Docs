# Фронтенд сервиса Везёт

[wiki](https://wiki.yandex-team.ru/taxi/frontend/frontent-vezjot/)

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/355397/info)

* NGINX - [taxifrontend-frontend-vezet](/services/taxifrontend-frontend-vezet/etc/nginx/sites-available/taxifrontend-frontend-vezet.conf)
* testing - [frontend-vezet.taxi.tst.yandex.net](https://frontend-vezet.taxi.tst.yandex.net)
* stable - [vezet.ru](https://vezet.ru)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка и разработка

- `cd services/taxifrontend-frontend-vezet/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
