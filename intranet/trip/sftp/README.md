## Описание
Сервис для походов по SFTP
Общение со внешним интернетом в основном сервисе происходит через GoZora, дырки в интернет нет.
GoZora не умеет проксировать запросы через SFTP, поэтому для хождения по SFTP используется
Код для отдельная сеть, у которой доступ во внешний интернет есть.

## Расположение
 - Deploy unit: `sftp`
 - https://deploy.yandex-team.ru/project/tools_trip_testing - Y.Deploy Тестинг
 - https://deploy.yandex-team.ru/project/tools_trip_production - Y.Deploy Продакшен

## Локальная разработка
 - `make arq` - поднять локалный сервер

## Deploy
 - `ya tool releaser release` - собрать и выкатить в тестинг sftp
 - `ya tool releaser deploy --stage tools_trip_production` - выкатить в продакшен

 Если нужно зарелизить sftp на стенд без changelog:
 - `make stand`

## В контейнере
 - `shell` - запустить ipython
