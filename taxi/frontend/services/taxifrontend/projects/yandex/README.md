# Фронтенд сервиса Яндекс.Такси

[wiki](https://wiki.yandex-team.ru/taxi/frontend/)

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354854/info)

* NGINX - [taxifrontend-taxi-frontend-yandex](/services/taxifrontend-taxi-frontend-yandex/etc/nginx/sites-available/taxifrontend-taxi-frontend-yandex.conf)

## Установка и разработка

- `cd services/taxifrontend-taxi-frontend-yandex/`
- `npm run install`
- `npm start`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Антиробот
[График андиробота на балансере](https://yasm.yandex-team.ru/template/panel/antirobot_for_service_with_req_group/req_group=taxi-frontend-yandex;service=taxi/)

### Админка - блога новостей
Тестинг: [https://l7test.yandex.ru/blog/taxi](https://l7test.yandex.ru/blog/taxi)

Продакшен: [https://yablogs-hidden.common.yandex.ru/taxi](https://yablogs-hidden.common.yandex.ru/taxi)

[wiki: документация](https://wiki.yandex-team.ru/taxi/web/Adminka-bloga-novostejj/)
