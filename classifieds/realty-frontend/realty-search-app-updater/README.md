# search-app-updater

Обновляет данные в YDB, откуда их читает search-app.

Описание работы `search-app`+`search-app-updater` находится в проекте `search-app`.

**ВАЖНО:** всегда будет запущено как минимум 2 экземпляра `search-app-updater`.
Чтобы периодические задачи не устраивали гонки, их синхронизация происходит через ZooKeeper.

## Основная информация

| Service | URL |
|---|---|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-search-app-updater |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-sa-updater |
| Grafana | **TODO** |

## Хосты

| Environment | URL |
|---|---|
| Testing | https://search-app-updater.realty.test.vertis.yandex.ru/ |
| Production | https://search-app-updater.realty.yandex.ru/ |

## Где что находится

[YDB UI testing](https://ydb.yandex-team.ru/db/ydb-ru-prestable/verticals/testing/common/browser) |
[YDB UI production](https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/realty/browser/rf-search-app/)

* testing DB: `/ru-prestable/verticals/testing/common`
* testing TablePrefix: `/ru-prestable/verticals/testing/common/rf-search-app`
* production DB: `/ru/verticals/production/realty`
* production TablePrefix: `/ru/verticals/production/realty/rf-search-app`

Ошибки YDB:
* [testing](https://ydb.yandex-team.ru/db/ydb-ru-prestable/verticals/testing/common/metrics/diagnostics)
* [production](https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/realty/metrics/diagnostics)

Схема таблицы `presets`
```sql
--!syntax_v1
PRAGMA TablePathPrefix("/ru-prestable/verticals/testing/common/rf-search-app");
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

* `make start-local` -  запуск

Для запуска отдельных скриптов можно использовать `node`:
```sh
$ node ./app/scripts/getRegionToUpdate.ts
```

Для подключения к YDB без TVM надо получить личный OAuth-ключ
и вставить `YDB_TOKEN` в `.env`. **Личный ключ нельзя коммитить!**
