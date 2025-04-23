# Фронтенд сервиса Скауты и Агенты

## Хосты

* NGINX - [hiring-scouts-n-agents](/services/hiring-scouts-n-agents/etc/nginx/sites-available/hiring-scouts-n-agents.conf)
* unstable - [scouts-n-agents.taxi.dev.yandex.net](http://scouts-n-agents.taxi.dev.yandex.net)
* testing - [scouts-n-agents.taxi.tst.yandex.net](http://scouts-n-agents.taxi.tst.yandex.net)
* stable - [scouts-n-agents.taxi.yandex.net](http://scouts-n-agents.taxi.yandex.net)
* stable - [scouts.prod.autodaniel.ru](https://scouts.prod.autodaniel.ru)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка

Общий регламент работы с монорепозиторием https://github.yandex-team.ru/search-interfaces/frontend#быстрый-старт

- `cd services/hiring-scouts-n-agents/`
- `npm run install`
- `npm start` 

## Сборка

- `npm run build:{ENV}` - ENV: stable | testing | unstable

## Релиз

[Как собирать и катитить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/)
