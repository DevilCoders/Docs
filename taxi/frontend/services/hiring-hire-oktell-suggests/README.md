# Фронтенд сервиса Ручки со списками для формы КЦ 

## Хосты
* NGINX - [hiring-hire-oktell-suggests](/services/hiring-hire-oktell-suggests/etc/nginx/sites-available/hiring-hire-oktell-suggests.conf)
* testing - [hire-oktell-suggests.taxi.tst.yandex.net](http://hire-oktell-suggests.taxi.tst.yandex.net)
* stable - [hire-oktell-suggests.taxi.yandex.net](http://hire-oktell-suggests.taxi.yandex.net)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка
Общий регламент работы с монорепозиторием https://github.yandex-team.ru/search-interfaces/frontend#быстрый-старт

- `cd services/hiring-hire-oktell-suggests/`
- `npm ci`

## Разработка
- `npm run install`
- `npm start` - 

## Сборка
- `npm run build:{ENV}` - ENV: stable | unstable

## Релиз
[Как собирать и катитить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/release/)
