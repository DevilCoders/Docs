# ClickHouse client

Клиент для clickhouse с поддержкой соединений для нескольких хостов. Основан на [@apla/clickhouse](npmjs.com/package/@apla/clickhouse)

## Использование

```js
const { ClickhouseStore } = require('@yandex-int/clickhouse-client');

const store = new ClickhouseStore({
    clients: [{
        host: 'some-clickhouse-host',
        auth: `some-user:some-password`,
        protocol: 'https:',
        port: 8443,
        rejectUnauthorized: false,
        queryOptions: {
            database: 'some-database',
        },
    }],
    // таблица, в которую будем пушить данные по умолчанию
    tableName: 'default-table',
    // Количество записей в чанке, которые будут вставлены за 1 запрос
    batchSize: 100,
    // Количество секунд перед отправкой данных в чанке
    batchInterval: 300, // по умолчанию Infinity
    // [RANDOM, ROUND_ROBIN]
    // Алгоритм выбора хостов. По умолчанию используется round robin
    connectionMode: 'RANDOM'
});

const rows = [
    {
        date_time: '2020-01-01 01:01:01',
        repo_full_name: 'search-interfaces/frontend'
    },
    {
        date_time: '2020-02-02 02:02:02',
        repo_full_name: 'search-interfaces/infratest'
    }
]

(async function () {
    store.setTableName('some-table');

    for (const row of rows) {
        await store.add({ ...row });
    }

    await store.flush();
})();
