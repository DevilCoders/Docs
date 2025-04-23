## Описание
Код для обработки внешней ручку из Аэроклуба

## Расположение
 - Deploy unit: `ext-api`
 - https://deploy.yandex-team.ru/project/tools_trip_testing - Y.Deploy Тестинг
 - https://deploy.yandex-team.ru/project/tools_trip_production - Y.Deploy Продакшен

## Локальная разработка
 - `ya make` - собрать бинарник
 - `ya make -tt` - запустить тесты
 - `make run` - поднять локалный сервер

## Deploy
 - `ya tool releaser release` - собрать и выкатить в тестинг ext-api
 - `ya tool releaser deploy --stage tools_trip_production` - выкатить в продакшен

 Если нужно зарелизить ext-api на стенд стенд без changelog:
 - `make stand`

## В контейнере
 - `shell` - запустить ipython
