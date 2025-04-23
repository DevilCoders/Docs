# Фронтенд сервиса Фронтенд разделов хэлпа

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [support-help-frontend](/services/support-help-frontend/etc/nginx)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

### TVM

Для разработки на вашу машину нужно скопировать секрет, куда копировать написано в самом [секрете](https://yav.yandex-team.ru/secret/sec-01f7kc0j2xhrngvzbmnbq7a08b/explore/versions)

### Запуск

use Nodejs >=14

- `cd services/support-help-frontend/`
- `npm install`
- `npm run prepare-dev-nginx`
- `npm run run`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Финтех

Для финтеха выгружается UATraits локально чтобы работал без доступа к сервису в qloud, чтоб выгрузка работала нужно чтобы был установлен [arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).
