## Контурная документация

Лежит на вики [вот тут](https://wiki.yandex-team.ru/non-adv-promotion/). В ней можно найти детали по микросервису и проектам. В частности, там же можно найти договоренности по стилям, liquibase скриптам и прочему.

## Локальный запуск
### Без TVM

1. Выполнить ``./localDatasources.sh``, который выкачает с braavos проперти datasources-ng-dev
2. Postgres
    ```
    mkdir -p $HOME/docker/volumes/postgres
    docker run --name adv_promo -e POSTGRES_PASSWORD=adv_promo -e POSTGRES_USER=adv_promo -h localhost -p 5433:5432 -d postgres
    ```
    Команды запустят PG на порте 5433, если нужно на другом порте, то вместо ``5433:5432`` нужно написать ``<port>:5432``

    Если какие-то из параметров для подключения к базе не стандартные (например, port или password), то их нужно изменить в local.properties

    Если на базу нужно накатить схему, то смотри раздел [Liquibase](#liquibase)
3. Запускаем ``ru.yandex.market.adv.promo.MarketAdvPromo`` в IDEA через main

### С TVM

1. Postgres и localDatasources (как в пред. пункте)
2. В local.properties меняем ``mbi.partner_tvm.tvm2.enabled`` на ``true``
3. В local.properties меняем ``adv.promo.tvm2.client_id`` на нужный:
    ```
    Тестинг: 2029676
    Прод: 2029883
    ```
4. В local.properties меняем ``adv.promo.tvm2.secret`` на секрет нужного окружения. Секрет можно найти в секретнице

    Секретница: [тестинг](https://yav.yandex-team.ru/secret/sec-01fcavw8sjewg93h89vj7nk2w9/explore/version/head), [прод](https://yav.yandex-team.ru/secret/sec-01fcavw7bqd5mpc696a34bz5dj/explore/version/head)
5. Запускаем ``ru.yandex.market.adv.promo.MarketAdvPromo`` в IDEA через main

### Накатка Liquibase

* Можно запустить скрипт liquibaseLocal.sh
    ```shell
    ./liquibaseLocal.sh
    ```
    В нем установлены стандартные данные для подключения к БД. Если нужны другие, то их можно добавить в переменные окружения:
    ```shell
    DB_HOST=localhost:port
    DB_NAME=name
    DB_USER=user
    DB_PASSWORD=password
    DB_SCHEMA=schema
    export DB_HOST DB_NAME DB_USER DB_PASSWORD DB_SCHEMA
    ```
* Можно в local.properties заменить ``spring.liquibase.enabled`` на ``true``, тогда накатка будет происходить автоматически при старте программы
