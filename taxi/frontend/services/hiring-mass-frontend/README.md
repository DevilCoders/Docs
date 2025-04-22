# Фронтенд сервиса Массовый найм (фронтенд)

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/39/edit/356236/info)

-   NGINX - [hiring-mass-frontend](/services/hiring-mass-frontend/etc/nginx/sites-available/hiring-mass-frontend.conf)
-   unstable - [TODO](host)
-   testing - [https://hiring-mass.taxi.tst.yandex-team.ru/](https://hiring-mass.taxi.tst.yandex-team.ru/)
-   stable - [https://hiring-mass.taxi.yandex-team.ru/](https://hiring-mass.taxi.yandex-team.ru/)

## Логи сервиса

| stable | testing |                                                                                       client |
| -----: | ------: | -------------------------------------------------------------------------------------------: |
|   TODO |    TODO | [error-booster](https://error.yandex-team.ru/projects/hiring-mass-frontend/projectDashboard) |

## Установка и разработка

### Предварительная настройка

скачать [файл настроек локального TVM демона](https://yav.yandex-team.ru/secret/sec-01fv2q80q79ne6a4srnvy7x65s/explore/versions) и положить в корень домашней папки пользователя с названием .tvm-hiring-mass-frontend (`~/.tvm-hiring-mass-frontend.json`)

### Запуск

`cd services/hiring-mass-frontend/`

`nvm use` (need nodejs 16)

`npm install -f`

`npm start`

## Сборка

`npm run build`

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
