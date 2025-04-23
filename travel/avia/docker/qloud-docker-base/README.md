# Ubuntu trusty

Базовый образ ubuntu для проектов avia.
Собран на основе базового образа ubuntu в Яндекс: registry.yandex.net/ubuntu:trusty

Включает в себя:
- nginx
- juggler
- geo-базу
- supervisord
- python 2.7 (gunicorn)
- solomon-agent
- push-client
- smailik
- jaeger-agent

Настроена ротация логов.

## Актуальная версия

Актуальную версию можно посмотреть в результатах последней sandbox-задачи: https://a.yandex-team.ru/projects/ticket/ci/actions/launches?dir=travel%2Favia%2Fdocker%2Fqloud-docker-base&id=build

## Сборка

```
ya package --docker --custom-version=unstable [--docker-push] pkg.json
```

`--docker-push` пушит образ в `registry.yandex.net/avia/ubuntu-trusty`

## Запуск

Команда запуска bash внутри контейнера:

```
docker run --env-file=dev.env -it registry.yandex.net/avia/ubuntu-trusty:unstable /bin/bash
```

## Публикация

```
docker push registry.yandex.net/avia/ubuntu-trusty:unstable
```
