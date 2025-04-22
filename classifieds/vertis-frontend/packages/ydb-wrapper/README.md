# @vertis/ydb-wrapper

Обертка над [ydb-sdk](https://www.npmjs.com/package/ydb-sdk)

* Пишет логи в формате [vertis-logs](https://wiki.yandex-team.ru/vertis-admin/logs/). `_context`: `ydb` и `ydb_error`
* Пишет в прометеус метрики: `ydb_request_duration_seconds{action="<action>"}` и `ydb_request_error{code="<code>"}`  
* Просто апи для запросов с ретраями

`prom-client` и `ydb-sdk` находятся в peerDependencies и должны быть установлены в проекте.

## Пример

```javascript
// ydb/driver.js
const { getDriver } = require('@vertis/ydb-wrapper');

const driver = getDriver({
    db: process.env.YDB_DB,
    entrypoint: process.env.YDB_ENTRYPOINT,
    connectTimeout: 10000,
    fallOnConnectError: true,
});

module.exports = driver;

// ydb/index.js
const { YdbWrapper } = require('@vertis/ydb-wrapper');
const driver = require('./driver');
const pino = require('@vertis/pino');

const ydb = new YdbWrapper(driver, {
    sessionTimeout: 100,
    tablePrefix: process.env.YDB_TABLE_PREFIX,
}, pino);

module.exports = ydb;

// <your file>.js
const ydb = require('./ydb/index');

function createTable() {
    return ydb.executeWithRetries(async(tablePathPrefix, session, logger) => {
        return session.createTable(
            tableName,
            new TableDescription()
                // ...
                // ...
        );
    }, { _context: 'createTable' });
}
```
