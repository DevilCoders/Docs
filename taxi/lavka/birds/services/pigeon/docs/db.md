# Работа с БД

* [Общая документация](../../../docs/db.md)

---

## Новый скрипт pgmigrate

*   Тип запускаемого скрипта: `pgmigrate`
*   Сервис: `lavka_pigeon`
*   Аргументы:

    Для **unstable, testing, production**

    ```
    --service_name=pigeon
    --db_name=pigeon
    --repository=taxi/lavka/birds
    --use-arc
    ```

    Для **unstable2**

    ```
    --service_name=pigeon
    --db_name=pigeon_unstable2
    --repository=taxi/lavka/birds
    --migrations-db-name=pigeon
    --use-arc
    ```

---

## Новый скрипт sql

*   Тип запускаемого скрипта: `psql`
*   Сервис: `lavka_pigeon`
*   Аргументы:

    ```
    --database-name=pigeon
    --psql-options=--echo-all
    ```

*   URL скрипта

    Сюда вставляем ссылку на скрипт, которую получили выше. Для testing и unstable можно использовать ссылку на ваш fork, но для стейбла можно использовать только скрипты из мастера

*   Посмотреть скрипты, которые уже запускались, можно так:

    * [production](https://tariff-editor.taxi.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Dpigeon)
    * [testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Dpigeon)
    * [unstable](https://tariff-editor.taxi.dev.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Dpigeon)

---

## CLI

*   ```bash
    # Сгенерировать новую миграцию
    pigeon db migration-create
    ```

*   ```bash
    # Локальный запуск миграций
    pigeon db migrate
    ```

---

## Накатить dump с тестинга на локальную БД

*   ```bash
    # с флагом -r получим свежий дамп тестинга
    pigeon db roll-testing-dump
    ```
