# Фронтенд сервиса Админка Найма

## Хосты

* NGINX - [hiring-admin-hiring](/services/hiring-admin-hiring/etc/nginx/sites-available/hiring-admin-hiring.conf)
* unstable - [admin-hiring.taxi.dev.yandex.net](https://admin-hiring.taxi.dev.yandex.net)
* testing - [admin-hiring.taxi.tst.yandex.net](https://admin-hiring.taxi.tst.yandex.net)
* stable - [admin-hiring.taxi.yandex.net](https://admin-hiring.taxi.yandex.net)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка

- `cd services/hiring-admin-hiring/`
- `npm run install`
- `npm start` 

## Сборка

- `npm run build:{ENV}` - ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/)
