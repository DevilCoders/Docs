# Contributing

## Предустановки

1. [Node.js](http://nodejs.org/)
2. [npm](http://npmjs.org)
3. [nvm](https://github.com/creationix/nvm)
4. [Docker](https://docs.docker.com/desktop/)
5. [ya](https://wiki.yandex-team.ru/yatool/)
6. postgresql
7. [yandex-pgmigrate](https://github.com/yandex/pgmigrate)

## Подготовка к разработке

1. Создать переменную окружения `MAPS_FRONT_STORIES_INT_TESTING_TVM_SECRET`:

    - Открыть https://yav.yandex-team.ru/?tags=maps-front-stories-int
    - Если к секрету нет доступа, запросить доступ в [ABC](https://abc.yandex-team.ru/services/maps-front-stories-int)
    - Перейти в секрет `maps-front-stories-int_testing`, найти ключ `TVM_SECRET`, скопировать в буфер.
    - Добавить в shell:

    ```sh
    export MAPS_FRONT_STORIES_INT_TESTING_TVM_SECRET=<секрет>
    ```

2. Создать переменную окружения `OAUTH_TOKEN`:

    - Открыть https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1
    - Добавить в shell:

    ```sh
    export OAUTH_TOKEN=<токен>
    ```

3. Создать переменную окружения `QTOOLS_TOKEN`:

    - Открыть https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4dd38b9acbb44ad8a7ece163ddf1c53a
    - Добавить в shell:

    ```sh
    export QTOOLS_TOKEN=<токен>
    ```

4. Создать переменную окружения `DCTL_YP_TOKEN`:

    - Открыть https://oauth.yandex-team.ru/authorize?response_type=token&client_id=688c92864835447b9ed74221f44420b7
    - Токен положить текстом в файл `~/.dctl/token`
    - Или как переменную окружения:

    ```sh
    export DCTL_YP_TOKEN=<токен>
    ```

5. Залогиниться в docker.registry
    - Читать: https://wiki.yandex-team.ru/qloud/docker-registry/#cli

## Запуск

1. Перейти к репозиторию

    ```sh
    cd /maps/front/services/stories-int
    ```

2. Переключиться на нужную версию Node.js:

    ```sh
    nvm use
    ```

3. Установить зависимости:

    ```sh
    make deps
    ```

4. Собрать и запустить прилождение в development режиме, используя database в docker:

    ```sh
    make dev-docker
    ```

    Так же вы можете поднять приложение без запуска базы данных (если вы уже поднимали её локально или в docker):

    ```sh
    make dev
    ```

По умолчанию приложение стартует на порту `http://localhost:8080/`

Изменить порт, на котором стартует приложение, можно в файле `dev.env`, или переопределите его, создав файл `dev-local.env`:

```sh
APP_PORT=8666
```

## Тестирование

Запустить все тесты с использованием локальной базы данных в docker:

```sh
make validate
```

## Деплой

### Автоматический деплой в testing

1. Создайте PR
2. Вмержьте его в `trunk`.

Новая версия приложение задеплоится в testing автоматически.

### Ручной деплой в testing

```sh
make patch # minor or major
make release-testing
```

### Ручной деплой в production

```sh
arc checkout trunk
arc pull trunk
arc rebase trunk

make release-production
```

## Миграция базы данных

1. Для локального запуска нужно предустановить [`yandex-pgmigrate`](https://github.com/yandex/pgmigrate)

```shell
brew install postgresql
pip install yandex-pgmigrate
pgmigrate --help
```

2. Запустить `make db-migrate-*`:
   — выполнятся все скрипты миграции из папки `/resources/db/migrations`
   — в табличке `schema_version` появятся записи об успешном выполнении каждого скрипта

## Шедулеры

## Регулярный импорт сторис для Я.Маркета

-   [README.md](src/schedulers/import-stories-by-url/README.md)
-   [CONTRIBUTING.md](src/schedulers/import-stories-by-url/CONTRIBUTING.md)

## Регулярное обновление геопоискового сниппета `stories_experimental/1.x`

-   [README.md](src/schedulers/activate-geosearch-snippets/README.md)
-   [CONTRIBUTING.md](src/schedulers/activate-geosearch-snippets/CONTRIBUTING.md)

## Style Guides

-   [TypeScript](https://github.com/ymaps/codestyle)
-   [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
