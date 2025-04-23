# Работа с БД

* [Общая документация](../../../docs/db.md)

---

## Новый скрипт pgmigrate

*   Тип запускаемого скрипта: `pgmigrate`
*   Сервис: `lavka_eagle`
*   Аргументы:

    Для **unstable, testing, production**

    ```
    --service_name=eagle
    --db_name=eagle
    --repository=taxi/lavka/birds
    --use-arc
    ```

* Посмотреть миграции которые уже раскатили можно так:

    * [production](https://tariff-editor.taxi.yandex-team.ru/dev/scripts?execute_type=pgmigrate&arguments=--service_name%3Deagle)
    * [testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts?execute_type=pgmigrate&arguments=--service_name%3Deagle)
    * [unstable](https://tariff-editor.taxi.dev.yandex-team.ru/dev/scripts?execute_type=pgmigrate&arguments=--service_name%3Deagle)

---

## Новый скрипт sql

*   Тип запускаемого скрипта: `psql`	
*   Сервис: `lavka_eagle`	
*   Аргументы:	

    ```	
    --database-name=eagle	
    --psql-options=--echo-all	
    ```	
*   URL скрипта	
    
    Сюда вставляем ссылку на скрипт, которую получили выше. Для testing и unstable можно использовать ссылку на ваш fork, но для стейбла можно использовать только скрипты из мастера

*   Посмотреть скрипты, которые уже запускались, можно так:
    
    * [production](https://tariff-editor.taxi.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Deagle)	
    * [testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Deagle)	
    * [unstable](https://tariff-editor.taxi.dev.yandex-team.ru/dev/scripts?execute_type=psql&arguments=--database-name%3Deagle)

---

## CLI

*   ```bash
    # Сгенерировать новую миграцию
    eagle db migration-create
    ```

*   ```bash
    # Локальный запуск миграций
    eagle db migrate
    ```

---

## Накатить dump с тестинга на локальную БД

*   ```bash
    # с флагом -r получим свежий дамп тестинга
    eagle db roll-testing-dump
    ```

---

## Консольный клиент для работы с базами

Для работы с базой можно использовать любой клиент к постгресу. Из консоли удобно использовать `psql`.

Чтобы его поставить

```bash
# macos
brew install postgresql
```

После установки можно подключаться к локальной базе командой

```bash
npm run dev:psql
```
