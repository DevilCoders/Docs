# Работа с БД

* [Общая документация](../../../docs/db.md)

---

## Новый скрипт pgmigrate

*   Тип запускаемого скрипта: `pgmigrate`
*   Сервис: `lavka_pigeonmarket`
*   Аргументы:

    Для **testing, production**

    ```
    --service_name=pigeon-market
    --db_name=pigeonmarket
    --repository=taxi/lavka/birds
    --migrations-db-name=pigeon-market
    --use-arc
    ```

---

## Новый скрипт sql

*   Тип запускаемого скрипта: `psql`
*   Сервис: `lavka_pigeonmarket`
*   Аргументы:

    ```
    --database-name=pigeonmarket
    --psql-options=--echo-all
    ```

*   URL скрипта

    Сюда вставляем ссылку на скрипт, которую получили выше. Для testing и unstable можно использовать ссылку на ваш fork, но для стейбла можно использовать только скрипты из мастера

*   Посмотреть скрипты, которые уже запускались, можно так:

    * [production](https://tariff-editor.taxi.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Dpigeonmarket)
    * [testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Dpigeonmarket)
