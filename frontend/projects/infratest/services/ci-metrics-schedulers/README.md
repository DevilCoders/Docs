# Набор шедулеров для сбора метрик CI

Собирают метрики с конвейера и складывают в ClickHouse [fei_infra]. Нужны до переезда в New CI.

[fei_infra]: https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-clickhouse/cluster/mdb93hb3hj9nthd6mme3?section=databases

## Существующие шедулеры

- [696563], [collect-frontend-builds.ts], [collect_frontend_builds.yaml] — собирает билды фронтенда с инфой, какие сервисы задеты

[696563]: https://sandbox.yandex-team.ru/scheduler/696563/view
[collect-frontend-builds.ts]: ./src/bin/collect-frontend-builds.ts
[collect_frontend_builds.yaml]: ../../.ci/schedulers/collect_frontend_builds.yaml

## Структура проекта

src/
- [`bin`](./src/bin) — код самих шедулеров
- [`lib`](./src/lib) — наборы вспомогательных файлов
- [`tables`](./src/tables) — описания табличек в CH, в которые мы складываем данные, и запросы для их создания в тестовом докере. Таблицы в проде создавайте вручную.
- [`__func__`](./src/__func__) — тесты
- [`__helpers__`](./src/__helpers__) — хелперы для тестов

## Запуск тестов

```sh
npm run build            # соберёт проект
npm run service:prepare  # поднимет докер с кликхаусом
npm run service          # запустит сами тесты
npm run service:shutdown # погасит докер с кликхаусом
```

В CI тесты запускаются в джобе `service`, т.к. это выделенная джоба с поднятием докеров.
