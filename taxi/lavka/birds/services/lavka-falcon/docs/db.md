# Работа с БД

* [Общая документация](../../../docs/db.md)

---

## Новый скрипт pgmigrate

*   Тип запускаемого скрипта: `pgmigrate`
*   Сервис: `lavka_lavka-falcon`
*   Аргументы:

    Для **unstable, testing, production**

    ```
    --service_name=lavka-falcon
    --db_name=lavka_falcon
    --repository=taxi/lavka/birds
    --use-arc
    ```

---

## Новый скрипт sql

*   Тип запускаемого скрипта: `psql`	
*   Сервис: `lavka_lavka-falcon`	
*   Аргументы:	

    ```	
    --database-name=lavka_falcon	
    --psql-options=--echo-all	
    ```	
*   URL скрипта	
    
    Сюда вставляем ссылку на скрипт, которую получили выше. Для testing и unstable можно использовать ссылку на ваш fork, но для стейбла можно использовать только скрипты из мастера

---

## CLI

*   ```bash
    # Сгенерировать новую миграцию
    falcon db migration-create
    ```

*   ```bash
    # Локальный запуск миграций
    falcon db migrate
    ```

---

## Накатить dump с тестинга на локальную БД

*   ```bash
    # с флагом -r получим свежий дамп тестинга
    falcom db roll-testing-dump
    ```
