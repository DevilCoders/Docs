# Ad feed

Сервис, генерирующий рекламные выборки.

## Выкат

Для выката нужно пользоваться утилитой `tools/deploy`.

Для выката всех модулей сразу:

    cd tools/deploy
    ya make -r
    ./deploy deploy-all --env={testing|preproduction|production} --root={path to ad_feed folder}

Для выката какого-то конкретного модуля:

    cd tools/deploy
    ya make -r
    ./deploy upload --env=testing --name={feed_name} --root={path to ad_feed folder}
    ./deploy deploy --env=testing --name={feed_name}

`feed_name` - имя фида, указанное в `bin/deploy/tasks.yaml`.

## Запуск

Для локального запуска можно воспользоваться командой

    ./deploy run --env=testing --name={feed_name} --root={path to ad_feed folder}

При запуске также подтянутся данные из файла конфигурации.

## Правила расстановки тегов на задачи в sandbox

`AD_FEED` - обязательный тег на все задачи.

`PRODUCTION`/`TESTING` в зависимости от контура.

На задачу со сборкой обязательно добавлять тег с названием sandbox-задачи, которую она собирает.

## Запуск тестов

Для запуска локальных тестов используйте `ya make -rtt`.

**Обратите внимание на флаг для релизной сборки!** Без него тесты mypy будут падать и долго работать.
