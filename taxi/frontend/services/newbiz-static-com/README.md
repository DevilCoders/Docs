# Фронтенд сервиса Статика сайта Яндекс Доставка для стран СНГ

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/151/edit/357432/info)

* [unstable](https://logistics-frontend.taxi.dev.yandex.com)
* [testing](https://logistics-frontend.taxi.tst.yandex.com)
* [stable](https://delivery.yandex.com)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Запрос роли ОКальщика релизов

https://nda.ya.ru/t/2AO9HQoE58iecC

## Установка и разработка

- `cd services/newbiz-static-com/`
- `npm ci`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
