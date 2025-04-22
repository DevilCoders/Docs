# search-app-updater

Обновляет данные в YDB, откуда их читает search-app.

Описание работы `search-app`+`search-app-updater` находится в проекте `search-app`.

**ВАЖНО:** всегда будет запущено как минимум 2 экземпляра `search-app-updater`.
Чтобы периодические задачи не устраивали гонки, их синхронизация происходит через ZooKeeper.

## Где что находится

[YDB UI testing](https://ydb.yandex-team.ru/db/ydb-ru-prestable/verticals/testing/common/browser) |
[YDB UI production](https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/autoru/browser/frontend)

* testing DB: `/ru-prestable/verticals/testing/common`
* testing TablePrefix: `/ru-prestable/verticals/testing/common/af-search-app`
* production DB: `/ru/verticals/production/autoru/frontend`
* production TablePrefix: `/ru/verticals/production/autoru/frontend/af-search-app`

Ошибки YDB:
* [production](https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/autoru/metrics/diagnostics)
* [testing](https://ydb.yandex-team.ru/db/ydb-ru-prestable/verticals/testing/common/metrics/diagnostics)

Схема таблицы `presets`
```sql
--!syntax_v1
PRAGMA TablePathPrefix("/ru-prestable/verticals/testing/common/af-search-app");
CREATE TABLE presets
(
    geo_id UInt32,
    preset Utf8,
    data Utf8,
    updated Datetime,
    PRIMARY KEY (geo_id, preset),
    INDEX updated_index GLOBAL ON (updated)
);
```

## Разработка

* `make` - сборка и запуск
* `make tsc` - сборка проекта
* `make tsc-watch` - запуск вотчера для пересборки TypeScript-файлов

Для запуска отдельных скриптов можно использовать `ts-node`:
```sh
$ YDB_TOKEN=<token> ../node_modules/.bin/ts-node -P tsconfig.json -r dotenv/config ./app/scripts/getRegionToUpdate.ts
```

## Различные скрипты для проверки/разработки

### checkZookeeperConnection

Проверяет соединение с `zookeeper`

```shell
$ cd www-search-app-updater
# Получаем секреты для подключения с zookeeper
$ make secrets
# Проверяем соединение и создание эфимерной ноды
$ npx ts-node app/scripts/checkZookeeperConnection.ts
# {"_level":"INFO","_time":"2022-01-23T16:17:44.636Z","_message":"[OK] Lock and Run"}
```
