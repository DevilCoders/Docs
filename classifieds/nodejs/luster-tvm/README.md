## luster-tvm

Плагин `luster` для работы с TVM. Мастер-процесс загружает и периодически подновляет ServiceTicket из TVM-API и рассылает их воркерам.

Инфо: https://wiki.yandex-team.ru/passport/tvm2/

### Подключение и настройка

`luster.conf.js`

```javascript
{
    extensions: {
        'luster-tvm': {
            // интервал обновления в ms (рекомендуется обновлять каждый час)
            refresh: 10 * 60000,
            // опции для запроса tvm-api (отправляются в asker как есть)
            connection: {
                requestId: 'luster-tvm',
                host: 'tvm-api.yandex.net',
                timeout: 500,
                maxRetries: 10,
                family: 6
            },
            // client id приложения
            src: '20100',
            // client secret приложения
            secret: 'somestring',
            // список client id приложений, для которых нужно получать тикеты
            dst: {
                passport: '20101',
                maps: '20102'
            }
        },
        
    }
}
```

### Usage

```javascript
const tvm = require('luster').tvm;
const tvmData = tvm.configureAPI();

const mapsServiceTicket = tvmData.getTicket('maps');
```

### API

```javascript
const tvm = require('luster').tvm;
```

#### `tvm.configureAPI(): Object`

```javascript
const tvmData = tvm.configureAPI();
```

#### `tvmData.getTicket(name: String): *`

```javascript
const mapsServiceTicket = tvmData.getTicket('maps');
```
