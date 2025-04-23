# Инфраструктура выкатки релизов и бет

## Сервисы фронта
Все сервисы, за которые ответственен фронтенд находятся в [Nanny](https://nanny.yandex-team.ru/ui/#/services).
Прод:
- `pdb-admin-nodejs-production-yp`: админка
- `pdb-nodejs-offline-prod-(man|sas|vla)-yp`: офлайн-сервис. Что-то навроде кэша, если бэк не отвечает
- `pdb-nodejs-production-(man|sas|vla)-yp`: сервисы, которые обрабатывают ответ пользователя
- `pdb-elastic-production-vla-yp`: сервис для логов фронтбека
- `pdb-kibana-production-yp`: UI-морда для сервиса логов

Тестинг:
- `pdb/features`: тестовые беты и "балансер" для бет
- `pdb-nodejs-prestable-yp`: prestable, шаблоны как на проде, ходит в продовый бэк. Виден на https://pdb-prestable.n.yandex.ru
- `pdb-nodejs-priemka-yp`: шаблоны как на проде, ходит в тестовый бэк. Виден на https://priemka.collections.test.yandex.ru. Нужен для асессоров.
- `pdb-admin-nodejs-test-yp`: тестовая админка
- `pdb-elastic-test-yp`: сервис для логов фронтбека
- `pdb-kibana-test-yp`: UI-морда для сервиса логов
- `pdb_nodejs_test`: шаблон для поднятия новой беты в ПР
- `pdb-nodejs-offline-test-yp`: офлайн-сервис тестинга
- `pdb-nodejs-test-yp`: тестовые шаблоны и тестовый бэк. Виден на https://l7test.yandex.ru/collections
- `pdb_nodejs_test_webapi`: ???

Не нужен:
- `pdb-storybook-yp`: когда-то использовался для сторибука

## Окружение асессоров
Ассессоры при тестировании ходят по ссылке https://collections-test.crowdtest.yandex.ru/collections/.

Стартовой точкой для окружения асессоров явлеяется [окружение](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/collections.crowdtest.yandex.ru/show) в awacs. Про awacs и определения можно почитать [здесь](https://wiki.yandex-team.ru/awacs/terminology).
Балансеры под webauth с `action: AUTHENTICATE_USING_IDM`. Это нужно для того, чтобы на тестинг могли попасть только те пользователяи, которым выдана роль асессора через IDM.
Окружение состоит из трех [upstreams](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/collections.crowdtest.yandex.ru/upstreams/list):
- default: обрабатывает все запросы
- https_avatars: перенаправляет запросы снаружи в тестовую аватарницу
- api: перенаправляет запросы на /api, /search, etc. на https://l7test.yandex.ru. Нужно, чтобы оставаясь на https://collections-test.crowdtest.yandex.ru/collections/ асессоры могли тестировать все части приложения (Избранное, СЕРП, Видео...) вместе.

**Ссылки**
- [Инструкция](https://docs.yandex-team.ru/direct-dev/reference/assessors/how-to-create-crowdtest-stand) по созданию окружения от Direct
- [Дока по асессорам](./../assessors/readme.md)


## Выкладка сервисов в Nanny
Создание сервисов и ресурсов начинается с npm-скрипта `ci:deploy`.
В нём запускается скрипт utils/deploy-development.sh. В этом скрипте по переменным окружения запускается процесс или для production-сборок, или для сборок тестинга/бет.

Далее кратко описано создание беты. Более подробно можно посмотреть в коде `utils/deploy-development.sh` и `utils/nanny`.
### Как создается бета в ПР
1. Запускаеся скрипт `ci:deploy` с YENV=testing
1. Заливается статика через `ci:deploy:static`
1. Собирается sandbox-ресурс `COLLECTIONS_FRONTEND_RESOURCE_TEST_PACKAGE` с кодом веб-сервера на koa внутри
1. Создается сервис (`pdb_nodejs_test_pr${number}`) в няне `utils/nanny/index.ts`
1. К сервису подвязывается созданный ресурс
1. Новый созданный сервис добавляется в `pdb-nodejs-feature-balancer-yp`
1. Бета работает

### Что происходит при отведении релиза
1. Запускается скрипт `ci:deploy` c YENV=production и с YENV=testing (чтобы обновить тестовые стенды)
1. Заливаеся статика через `ci:deploy:static`
1. Собирается sandbox-ресурс `COLLECTIONS_FRONTEND_RESOURCE_TEST_PACKAGE` (тест) и `COLLECTIONS_FRONTEND_RESOURCE_PACKAGE` (прод) с кодом веб-сервера на koa внутри
1. При переменной YENV=production создается таска [COLLECTIONS_FRONTEND_RELEASE](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/collections/CollectionsFrontendRelease/__init__.py), в которую передается id ресурса `COLLECTIONS_FRONTEND_RESOURCE_TEST_PACKAGE`
1. `COLLECTIONS_FRONTEND_RELEASE` копирует себе этот ресурс. Эта задача нужна для связывания ресурса c релизом в nanny через [TicketIntegration](https://docs.yandex-team.ru/nanny/how-to/sandbox-integration)
1. Пример TI: https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-offline-prod-sas-yp/tickets_integration
1. Здесь автоматика заканчивает работать и начинаются ручные действия
