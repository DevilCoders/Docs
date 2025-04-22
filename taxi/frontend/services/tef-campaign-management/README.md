# Фронтенд сервиса Campaign management

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354150/info)

* NGINX - [tef-campaign-management](/services/tef-campaign-management/etc/nginx/sites-available/tef-campaign-management.conf)
* unstable - [campaign-management-unstable.taxi.tst.yandex-team.ru](https://campaign-management-unstable.taxi.tst.yandex-team.ru/)
* testing - [campaign-management.taxi.tst.yandex-team.ru](https://campaign-management.taxi.tst.yandex-team.ru/)
* testing - [cm.taxi.tst.yandex-team.ru](https://cm.taxi.tst.yandex-team.ru/)
* stable - [campaign-management.taxi.yandex-team.ru](https://campaign-management.taxi.yandex-team.ru/)
* stable - [cm.taxi.yandex-team.ru](https://cm.taxi.yandex-team.ru/)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка
- скачать архив с сертификатами из [yav](https://yav.yandex-team.ru/secret/sec-01g4f455x5nrh56hjjcc2kjhfp) 
- распаковать архив в папку cert
- `cd services/tef-campaign-management/`
- `npm run install`
- `npm run run` — запуск на дев-машинке
- `npm run run:local` — запуск локально

## Сборка

- `npm run build:{ENV}` - ENV: stable | testing | unstable

## Релиз

[Как собирать и катитить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Техническая документация

- [Собственная конфигурация дев-сервера](docs/customDevServerConfig.md)
- [Нюансы / проблемы, связанные с датами](docs/datetimeFields.md)
- [Автоматическая генерация типов](docs/typesGeneration.md)
- [Обработка ошибок](docs/errorHandling.md)
