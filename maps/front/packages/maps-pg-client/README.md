# maps-pg-client

NPM-модуль для работы с базой данных на основе [node-postgres](https://node-postgres.com). В NPM-модуле происходит автоматический поиск мастера и наиболее выгодной реплики на основе прямых подключений к базам через `hosts`. Node-postgresql пока не умеет работать с мультихостами (https://github.com/brianc/node-postgres/pull/1711).

## Установка

```
npm install @yandex-int/maps-pg-client --registry http://npm.yandex-team.ru --save
```

## Использование

```js
import {MapsPgClient} from '@yandex-int/maps-pg-client';
const dbClient = new MapsPgClient({
    pgPoolSettings: {
        user: 'podrik',
        password: '123456',
        database: 'databaseName',
        ssl: {cert: 'cert.pem'},
        port: 6432,
        connectionTimeoutMillis: 10000,
        max: 5,
        idleTimeoutMillis: 120000
    },
    hosts: [host1, host2, host3],
    dbErrorHandler: (err) => console.error(err)
});


dbClient.executeReadQuery('SELECT * from table;');
dbClient.executeReadCallback(async (client) => {
    const result = await client.query('SELECT * from table;');
    return result;
});
dbClient.executeWriteQuery('INSERT INTO table DEFAULT VALUES');
dbClient.executeWriteCallback(async (client) => {
    await client.query('SELECT * from table;')
});
```

## API
**new MapsPgClient(options)**
* `options.pgPoolSettings` — конфиг для [pg.Pool](https://node-postgres.com/api/pool).
* `options.hosts` — массив доступных хостов, прямые подключения к базам данных (master, replicas).
* `options.dbErrorHandler` — функция, которая обрабатывает ошибки. Логирование.
* `options.settings` — не обязательные настройки, перечислены ниже.
* `options.settings.failCountLimit` — количество раз, которое не учитывается, если подключение к pg.Pool дало ошибку. По умолчанию, 1.
* `options.settings.checkPoolTime` — Время в ms через которое проверяются пуллы. По умолчанию, 3000.
* `options.settings.maxExecuteTime` — Максимальное время в ms, которое ожидается при выполнении запроса на проверку пулла. По умолчанию, 3000.

**Важно!!!**
1. У каждой базы есть лимит на количество подключений, не у кластера, лимиты можно посмотреть [здесь](https://wiki.yandex-team.ru/mdb/faq/faqpgsql/#kakieznachenijapo-umolchanijuuparametrovmaxconnectionsisharedbufferskakieogranichenijaposeti). Необходимо проставлять `options.pgPoolSettings.max`, которое рассчитывается как `Math.floor((max_connections - 10 (резерв для пингов)) / кол-во инстансов)`. Например, для db1.nano: `(50 - 10)/3 = 13`. По умолчанию, `max = 10`.

2. `options.pgPoolSettings.host` не будет учитываться. Все хосты необходимо перечислять в `options.hosts`.
