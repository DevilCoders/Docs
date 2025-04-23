# Фронтенд сервиса GreenplumDB Manager 

Мониторинг запросов пользователей, ETL сервисов, утилизации ресурсов кластера

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [tef-greenplum-frontend](/services/tef-greenplum-frontend/etc/nginx/sites-available/tef-greenplum-frontend.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

- скачать архив с сертификатами из [yav](https://yav.yandex-team.ru/secret/sec-01g4f455x5nrh56hjjcc2kjhfp)
- распаковать архив в папку cert
- `cd services/tef-greenplum-frontend/`
- `npm run install`
- `npm run run` — запуск на дев-машинке
- `npm run run:local` — запуск локально

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Техническая документация

- [Автоматическая генерация типов](docs/typesGeneration.md)
