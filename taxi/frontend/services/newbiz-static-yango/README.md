# Фронтенд сервиса Статика сайта Яндекс Доставка на международном рынке

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/151/edit/357431/info)

* NGINX - [newbiz-static-yango](/services/newbiz-static-yango/etc/nginx/sites-available/newbiz-static-yango.conf)
* [unstable](https://logistics-frontend.dev.yango.delivery)
* [testing](https://logistics-frontend.tst.yango.delivery)
* [stable](https://yango.delivery)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Запрос роли ОКальщика релизов

https://nda.ya.ru/t/ftp7g4OW58icM8

## Установка и разработка

- `cd services/newbiz-static-yango/`
- `npm ci`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
