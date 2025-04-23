## Medium тесты cdp-api

### Цели

Хотелось (и получилось) добиться трёх вещей:
 - Иметь возможность стартовать и тестировать как всё api (полный Spring контекст), так и отдельные классы требующие
   внешних систем
 - Иметь возможность запустить тест из IDEA
 - Получить честную полную изоляцию, всё окружение обложить рецептами

### Необходимое для запуска cdp-api окружение
 - YDB
 - Logbroker
 - MySQL (5.7 +)
   * Тут есть нюанс: для старта API нужен не просто какой-то MySQL, а еще куча конкретных таблиц в нём
   и не редко еще и какие-то данные в них. Здесь было принято решение положить всё необходимое в `.sql` файлы
   прямо в коде и создавать схему во время старта тестов. Файлы лежат по адресу `../cdp-api/src/test_lagre/ru/yandex/metrika/cdp/api/tests/large/mysql/`
 - PostgreSQL
 - Clickhouse

### Запуск через "аркадийные" тесты
Начнём с простого
```
ya make -ttt
```

### Запуск из IDEA

Тут сложнее, чем в предыдущем пункте. Есть две магические палочки для запуска "аркадийных" тестов с рецептами из IDEA:
 - Docker вместо рецептов
 - "Умные" дефолты

#### Docker вместо рецептов
На самом деле это иногда Docker вместо рецептов, а иногда Docker у которого внутри рецепт, но это не принципиально.

Запустить можно сделать как с локального компа, так и с виртуалки (в QYP например).

```bash
docker run --name=postgres-dev-server --env=POSTGRES_PASSWORD=password --env=POSTGRES_USER=metrika --env=POSTGRES_DB=test -p 5432:5432 --restart=always --detach=true postgres
docker run --name=mysql-dev-server --env=MYSQL_ROOT_PASSWORD=root --env=MYSQL_DATABASE=test --env=MYSQL_USER=metrika --env=MYSQL_PASSWORD=password -p 3306:3306 --restart=always --detach=true mysql:5.7
docker run --name=clickhouse-dev-server -p 8123:8123 --restart=always --detach=true yandex/clickhouse-server
docker run --name=ydb-dev-server --hostname=`hostname` -p 2135:2135 --restart=always --detach=true registry.yandex.net/yandex-docker-local-ydb:stable
docker run --name=lbk-dev-server --hostname=`hostname` --env=LOGBROKER_CREATE_TOPICS=metrika/cdp/cdp-clients-topic,metrika/cdp/cdp-orders-topic --env GRPC_PORT=2136 -p 2136:2136  --restart=always --detach=true registry.yandex.net/yandex-docker-local-lbk
```

#### "Умные" дефолты

Есть класс `EnvironmentHelper`, которые умеет
- определить находимся ли мы сейчас в "аркадийном" тесте
- если да, то распарсить все переменные окружении, заданные рецептами, и положить их в локальные переменные
- если нет, то заполнить локальные переменные "умными" дефолтами, а именно:
  * у каждой переменной есть "умный" дефолт (в основном, очевидные вещи, типо хост - `localhost`, дефолтные порты для баз и т.д.)
  * есть опциональный файлик, который может лежать на локальной файловой системе по пути `~/.metrika/tests/default.properties`,
    в котором можно переопределить дефолты. Таким образом можно добиться чтобы тесты ходили в произвольное тестовое окружение
    при запуске из IDEA. Например, для запуска Docker образов на виртуалке в QYP, командами указанными выше, локальный
    файл выглядит следующим образом:
    ```
    DEFAULT_HOST=${здесь FQDN виртуалки}
    LOGBROKER_PORT=2136
    POSTGRES_RECIPE_USER=metrika
    POSTGRES_RECIPE_PASSWORD=password
    POSTGRES_RECIPE_DBNAME=test
    ```
