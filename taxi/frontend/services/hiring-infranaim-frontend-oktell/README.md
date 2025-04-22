# Фронтенд сервиса Форма найма в КЦ oktell 3.0

Сервис для обработки звонков при общении с водителями / курьерами и тд.

## Хосты

* NGINX - [hiring-infranaim-frontend-oktell](/services/hiring-infranaim-frontend-oktell/etc/nginx/sites-available/hiring-infranaim-frontend-oktell.conf)
* unstable - [infranaim-frontend-oktell.taxi.dev.yandex.net](https://infranaim-frontend-oktell.taxi.dev.yandex.net/v3/)
* testing - [infranaim-frontend-oktell.taxi.tst.yandex.net](https://infranaim-frontend-oktell.taxi.tst.yandex.net/v3/)
* stable - [infranaim-frontend-oktell.taxi.yandex.net](https://infranaim-frontend-oktell.taxi.yandex.net/v3/)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка

Общий регламент работы с монорепозиторием https://github.yandex-team.ru/search-interfaces/frontend#быстрый-старт

- `cd services/hiring-infranaim-frontend-oktell/`
- `npm ci`

## Разработка

- `npm run install`
- `npm start` - 

## Сборка

- `npm run build:{ENV}` - ENV: stable | unstable

## Релиз

[Как собирать и катитить релиз (TODO)](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/)
