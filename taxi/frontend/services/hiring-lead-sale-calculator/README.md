# Фронтенд сервиса Форма продажи лидов

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [hiring-lead-sale-calculator](/services/hiring-lead-sale-calculator/etc/nginx/sites-available/hiring-lead-sale-calculator.conf)
* testing - [lead-sale-calculator.taxi.tst.yandex.net](https://lead-sale-calculator.taxi.tst.yandex.net)
* stable - [lead-sale-calculator.taxi.yandex.net](https://lead-sale-calculator.taxi.yandex.net)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка и разработка

- `cd services/hiring-lead-sale-calculator/`
- `npm run install`

Перед запуском сделайте файл `.env` на основе `.env.example` и положите в перменную `CALC_TOKEN` значение из [yav](https://yav.yandex-team.ru/secret/sec-01ed6v1ndaxqf0q14zxhajjqrq).

- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
