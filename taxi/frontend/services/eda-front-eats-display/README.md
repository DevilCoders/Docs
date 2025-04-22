# Фронтенд сервиса Дисплей Еды

Витрина метрик Яндекс.Еды для отображения на телевизорах, а так же обычного захода пользователей

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/36/edit/356369/info)

* testing - [http://front-eats-display.eda.tst.yandex.net](http://front-eats-display.eda.tst.yandex.net)
* stable - [http://front-eats-display.eda.yandex.net](http://front-eats-display.eda.yandex.net)

## Установка и разработка

- `cd services/eda-front-eats-display/`
- `npm run install`
- `touch .env`
- Скопировать токен из [секретницы](https://yav.yandex-team.ru/secret/sec-01fvy8ek88k8f2epeq89nw7pte/explore/version/ver-01fvy8ek8njw2d71mr450t427b) и положить в файл `.env` как:
```env
YT_ROBOT_AUTH_TOKEN=значение_токена
```
- `npm run dev` - Для разработки фронт + бэк вместе
- Если отдельно, то
  - `npm run settings:build:development` - Для подготовки настроек
  - `npm run frontend:dev` - Запуск фронта в режиме разработки
  - `npm run server:dev` - Запуск сервера в режиме разработки
- Фронтовый DevServer открывается на `8080` порту, сервер на `3000`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
