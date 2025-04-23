## Расположение
 - https://deploy.yandex-team.ru/project/tools_trip_testing - Y.Deploy Тестинг
 - https://deploy.yandex-team.ru/project/tools_trip_production - Y.Deploy Продакшен

## Локальная разработка
 - `ya make` - собрать бинарник
 - `ya make -tt` - запустить тесты
 - `docker-compose up -d` - поднять локальную базу
 - `make run` - поднять локалный сервер
 - `make shell` - запустить ipython
 - `make dbshell` - запустить psql

## Deploy
 - `make testing` - собрать и выкатить в тестинг
 - `make deploy-migration` - выкатить деплой юнит migration в продакшене (необходим для применения миграций до выкатки кода в юните api)
 - `make production` - выкатить в продакшен

 Если нужно зарелизить стенд без changelog:
 - `make stand`

## Миграции
 - `alembic/trip.alembic revision --message="<message>" --autogenerate` - создать файл миграции локально
 - `alembic/trip.alembic upgrade head` - выполнить миграции локально
 - `/trip-db upgrade head` - выполнить миграции в Box в Y.Deploy

Чтобы в боксе были переменные окружения, необходимо выкатывать релиз по этой инструкции: https://st.yandex-team.ru/COMMONPY-263#5eb3f4497b4aea4b046cfdb0

## В контейнере
 - `shell` - запустить ipython
 - `dbshell` - запустить psql

#### Настройка PyCharm
1. Поставить плагин: https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/README.md
2. Настроить удаленный интерпретатор: https://sulim.at.yandex-team.ru/187

#### Проверка квоты
`ya tool yp_util account explain abc:service:31132 --cluster SAS`

#### Алерты
В корне лежит конфиг .monitorado.yml

Дока https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado/README.md

#### Дашборд
1. Основной https://yasm.yandex-team.ru/panel/d1568.trip-dashboard/
2. Unistat https://yasm.yandex-team.ru/panel/d1568._pCFOPQ
