## Расположение
 - https://deploy.yandex-team.ru/project/watcher-test - Y.Deploy Тестинг
 - https://deploy.yandex-team.ru/project/watcher-prod - Y.Deploy Продакшен

## Локальная разработка
 - `ya make` - собрать бинарник
 - `ya make -tt` - запустить тесты
 - `docker-compose up -d` - поднять локальную базу (так же можно postgres.app поставить)
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
Для создания миграций с актуальной версией кода без пересборки бинарника можно использовать
`export Y_PYTHON_SOURCE_ROOT=<путь_до_аркадии>`
 - `alembic/watcher.alembic revision --message="<message>" --autogenerate` - создать файл миграции локально
 - `alembic/watcher.alembic upgrade head` - выполнить миграции локально
 - `alembic/watcher.alembic current` - текущее состояние
 - `alembic/watcher.alembic history` - история миграций
 - `/watcher-db upgrade head` - выполнить миграции в Box в Y.Deploy

## В контейнере
 - `shell` - запустить ipython
 - `dbshell` - запустить psql


#### Алерты
В корне лежит конфиг .monitorado.yml

Дока https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado/README.md
