# Как работает наш CI

## Prerequisites

1. [Trendbox](https://github.yandex-team.ru/search-interfaces/trendbox-ci/blob/master/docs/formats/0.2/configuration-reference.md)
2. [Sandbox](https://wiki.yandex-team.ru/sandbox/tasks/)
3. [TKit](https://a.yandex-team.ru/arc_vcs/maps/front/packages/tkit)

## Общая схема

Для того, чтобы запустить CI, GitHub отправляет событие в вебхук сервиса Trendbox. Trendbox в свою очередь запускает задачу в Sandbox, которая исполняет скрипт `tools/ci.js`, конфигурирует и запускает TKit.

По мере выполнения в интерфейсе гитхаба прокрашиваются статус-чеки.
Красный крестик — статус-чек завершил свою работу с ошибкой.
Зеленая галочка — все хорошо.
Желтый кружочек — задача в процессе выполнения.

Ключевые этапы: установка зависимостей (DEPS) -> сборка бандла (BUILD) -> поднятие стенда (DEPLOY_STAND) -> запуск автотестов (HERMIONE).

## Переменные окружения

Если в задаче нужно использовать переменные окружения, которые не хочется хранить в коде (например секреты), используйте [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault).

Чтобы добавить новую переменную окружения для использования внутри какого-то из скриптов, вызывающегося из `tools/ci.js`, нужно добавить новый секрет в [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault). Он должен начинаться с префикса `env.`, например `env.YOUR_VARIABLE_NAME`, и в поле `Shared With` нужно указать название нашей группы в сендбоксе: `MAPS_FRONT`.

После этого ваша переменная окружения будет добавлена в контейнер, в котором запускается задача в Sandbox.

## Деплой стендов

Все наши стенды используют единый докер-образ. Чтобы увидеть список доступных версий образа, можно выполнить команду

```
curl -X GET \
  https://registry.yandex.net/v2/maps/front-maps-stand-base/tags/list \
  -H 'Authorization: OAuth YOUR_TOKEN_HERE'
```

(Токен можно получить [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1))

Преимущества — улучшенное кеширование, образ почти всегда уже лежит на хостах, где деплоятся наши стенды.

### Внесение изменений в докер-образ

Наш докерфайл использует multistage build. Локально — вместе с `DOCKER_BUILDKIT=1` (Docker 18.09+).

Без указания `DOCKER_BUILDKIT=1` докер будет собирать образ последовательно, включая неиспользуемые слои.

Наглядно:

| Команда                                                | Порядок сборки              |
| ------------------------------------------------------ | --------------------------- |
| `docker build . --target=production`                   | base -> production          |
| `docker build . --target=stand`                        | base -> stand -> production |
| `DOCKER_BUILDKIT=1 docker build . --target=production` | base -> production          |
| `DOCKER_BUILDKIT=1 docker build . --target=stand`      | base -> stand               |

`base` используется и в `production`, поэтому изменения в нем следует делать с особой осторожностью.

После внесения изменений в стейджи `base` или `stand`, запустите команду `make update-stand-image` и сделайте коммит изменений.

После внесения изменений в стейджи `base` или `production`, запустите команду `make update-production-image` и сделайте коммит изменений.

Эта команда соберет и опубликует докер-образ, а так же обновит его тег в соотвествующем файле `stand.version` или `production.version`.

**ВАЖНО**: стоит помнить, что `dockerignore.stand` хранит в себе контекст для докера стендовой версии, и он отличен от продакшена. Изменения контекста, необходимые только для `--target=stand` нужно сохранять именно в этом файле.
