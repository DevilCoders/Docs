# Admin Lenta

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/150/edit/355355/deployments)

* NGINX - [lenta](/services/admin-lenta/etc/nginx/sites-available/admin-lenta.conf)
* dev - [https://lenta.taxi.localhost.yandex.ru:4200](https://lenta.taxi.localhost.yandex.ru:4200)
* testing - [lenta.taxi.tst.yandex.ru](https://lenta.taxi.tst.yandex.ru)
* stable - [lenta.taxi.yandex.ru](https://lenta.taxi.yandex.ru)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка и разработка
- `cd services/admin-lenta/`  
Взять токен [отсюда](https://yav.yandex-team.ru/secret/sec-01f0zkd5mf7pm5z7tvj39gdk40), положить в корень проекта и сделать:  
- `npm run init`

## TVM
Для локальной разработки:
- скопировать .tvm.json в корень проекта отсюда https://yav.yandex-team.ru/edit/secret/sec-01f0zkd5mf7pm5z7tvj39gdk40/explore/version/ver-01f0znjd5mmsyskr5j81xfed04
- создать директорию /.certs в проекте и добавить файл dev.pem отсюда https://yav.yandex-team.ru/secret/sec-01fz87kn49trh0wmvyb2yxrk37/explore/version/ver-01fz87kn4s09smhhwm7q11f9fa

### Запуск
```bash
~$ npm run dev
```

Смотреть после запуска тут: [https://lenta.taxi.localhost.yandex-team.ru:4210](https://lenta.taxi.localhost.yandex-team.ru:4210/).

## Сборка

- `npm run build:production`

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
