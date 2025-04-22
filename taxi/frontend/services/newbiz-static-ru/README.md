# Фронтенд сервиса 

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [newbiz-static-ru](/services/newbiz-static-ru/etc/nginx/sites-available/newbiz-static-ru.conf)
* [unstable](https://logistics-frontend.taxi.dev.yandex.ru)
* [testing](https://logistics-frontend.taxi.tst.yandex.ru)
* [stable](https://dostavka.yandex.ru)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

- `cd services/newbiz-static-ru/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
