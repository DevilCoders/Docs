# Фронтенд сервиса Саморегистрация курьеров

## Хосты

* NGINX - [hiring-courier-selfreg](/services/hiring-courier-selfreg/etc/nginx/sites-available/hiring-courier-selfreg.conf)
* unstable - [courier-selfreg.eda.dev.yandex.net](http://courier-selfreg.eda.dev.yandex.net/)
* testing - [courier-selfreg.eda.tst.yandex.net](http://courier-selfreg.eda.tst.yandex.net/)
* stable - [courier-selfreg.eda.yandex.net](http://courier-selfreg.eda.yandex.net/)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка

- `cd services/hiring-courier-selfreg/`
- `npm run install`
- `npm start` - запуск dev-сервера 

## Сборка

- `npm run build:{ENV}` - ENV: stable | testing | unstable

## Релиз

[Как собирать и катитить релиз (TODO)](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/)
