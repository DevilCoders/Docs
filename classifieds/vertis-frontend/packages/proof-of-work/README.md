# @vertis/proof-of-work

Код для [proof-of-work](https://github.com/indutny/proof-of-work) для защиты от тупых парсеров.

## Подключение в проект

### Установка
```
npm install --save @vertis/proof-of-work 
```

### webpack

В конфиге webpack для клиентского бандла надо подключить [worker-loader](https://github.com/webpack-contrib/worker-loader). Пример:
```
{
    test: /\.worker\.js$/,
    use: isServer || isPuppeteer ?
        'null-loader' :
        {
            loader: 'worker-loader',
            options: {
                // подробнее https://github.com/webpack-contrib/worker-loader#inline 
                inline: 'no-fallback',
            },
        },
},
```

### Использование

1. Клиент формирует payload (например, ID объявления), запрашивает на сервере nonce, потом формирует хэш.
```js
const { calcProofOfWorkHash } = require('@vertis/proof-of-work/client');

module.exports = (params) => {
    const payload = params.someProjectPayload;
    return getProofOfWorkNonce(payload)
        .then((pow) => {
            const requestParams = { ...params, pow };
            return fetch('/phones', requestParams);
        });
};

function getProofOfWorkNonce(payload) {
    if (typeof Worker !== 'function') {
        return Promise.resolve(false);
    }

    return fetch('/pow_nonce', { payload })
        .then(async({ nonce, timestamp }) => {
            const { hash, time } = await calcProofOfWorkHash({ nonce: nonce });
            return { hash, time, timestamp, payload, client_timestamp: Date.now() };
        })
        .catch((error) => {
            if (typeof Ya !== 'undefined' && typeof Ya.Rum !== 'undefined') {
                Ya.Rum.logError(
                    { block: 'pow', type: 'logic' },
                    error,
                );
            }

            return Promise.resolve(false);
        });
}

```

2. Ручка `/pow_nonce` выглядит на сервере вот так:
```js
const { createSignNonce } = require('@vertis/proof-of-work');

const salt = process.env.PROOF_OF_WORK_SALT;

function getPoWNonce(payload) {
    if (typeof payload !== 'string') {
        // HTTP 400 response
        return throw new Error('BAD_REQUEST');
    }

    const timestamp = Date.now();
    const prefix = createSignNonce({ payload, timestamp, salt });

    return {
        nonce: prefix,
        timestamp: timestamp,
    };
}
```

3. Проверка хэша на сервере выглядит вот так:
```js
const { validateHash } = require('@vertis/proof-of-work');

const salt = process.env.PROOF_OF_WORK_SALT;

function getPhones(params) {
    const { pow, timestamp, payload } = params;
    if (!pow) {
        // PoW нет - HTTP 403 response
        return throw new Error('BAD_REQUEST');
    }

    const powValidateResult = validateHash({ hash: pow, timestamp, payload, salt });
    if (!powValidateResult) {
        // PoW не прошел валидацию - HTTP 403 response
        return throw new Error('BAD_REQUEST');
    }
    
    // backend request
}
```

Еще можно завести себе гистограмму
```
const promClient = require('prom-client');
const powResultHistogram = new promClient.Histogram({
    name: 'pow_result',
    help: 'PoW check result',
    labelNames: [ 'browser', 'os', 'result' ],
    buckets: [ 1, 2, 3, 4, 5, 10, 15, 20 ],
});

powResultHistogram.observe({
    browser: req.browser.BrowserName,
    os: req.browser.OSFamily,
    result: String(powValidateResult),
}, (Number(pow.time) || 0) / 1000);
```
