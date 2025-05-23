# Contributing

## Разработка

1. Переключить на нужную версию Node.js, указанную в `.nvmrc`:

    ```sh
    nvm use
    ```

2. Установить зависимости:

    ```sh
    make deps
    ```

3. Убедиться, что по пути `~/.ssl/ssl.crt` есть сертификат. Нужен, чтобы делать запросы в тестовую базу данных с локальной машины. Если сертификат находится по другому пути, отредактируйте переменные окружения в [Makefile](./Makefile)

4. Запустить скрипт testing-окружения:

    ```sh
    make dev
    ```

## Релиз

1. Собрать js-код:

    ```sh
    make build
    ```

2. Проверить, что собранный скрипт работает корректно. Шедулер запустится для testing-окружения:

    ```sh
    make dev-builded
    ```

3. Поднять версию шедулера и запаблишить его в Sandbox

    ```sh
    make patch
    ```

    Эта команда сама вызовет `npm preversion` и `npm postversion` (см. `package.json`)
