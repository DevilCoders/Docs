# Ubuntu bionic

Базовый образ ubuntu для проектов avia.
Собран на основе базового образа ubuntu в Яндекс: registry.yandex.net/ubuntu:bionic

Включает в себя:
- nginx
- supervisord
- solomon-agent
- python 2.7 (sideeffect, напрямую не устанавливается)
- python 3.6 (aka python3)
- python 3.7
- push-client
- jaeger-agent

Настроена ротация логов.

## Актуальная версия

Актуальную версию можно посмотреть в результатах последней ci сборки: https://a.yandex-team.ru/projects/ticket/ci/actions/launches?dir=travel%2Favia%2Fdocker%2Fdeploy-docker-base-bionic&id=build

## Сборка

```
ya package --docker --custom-version=unstable [--docker-push] pkg.json
```

`--docker-push` пушит образ в `registry.yandex.net/avia/ubuntu-trusty`

## Запуск

Команда запуска bash внутри контейнера:

```
docker run --env-file=dev.env -it registry.yandex.net/avia/ubuntu-bionic-deploy:unstable /bin/bash
```

## Публикация

```
docker push registry.yandex.net/avia/ubuntu-bionic-deploy:unstable
```
