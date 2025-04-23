# Express TVM middleware
![](https://badger.yandex-team.ru/npm/@yandex-int/express-tvm/version.svg)
![](https://badger.yandex-team.ru/npm/@yandex-int/express-tvm/owner.svg)
[![oko express-tvm](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/express-tvm)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/express-tvm)

Миддлвара для получения TVM тикетов в `req.tvm`.

- [Установка](#установка)
- [Подключение локально](#подключение-локально)
- [Подключение для сервиса в Qloud](#подключение-для-сервиса-в-qloud)
- [Опции](#опции)
  - [cacheMaxAge](#cachemaxage)
  - [cacheKeyHeaders](#cachekeyheaders)
  - [cacheKeyQueryParams](#cachekeyqueryparams)
  - [clientId (required)](#clientid-required)
  - [destinations (required)](#destinations-required)
    - [Как массив](#как-массив)
    - [Как объект](#как-объект)
  - [serverUrl (required)](#serverurl-required)
  - [keepAlive](#keepalive)
  - [logger](#logger)
  - [logError](#logerror)
  - [retry](#retry)
  - [timeout](#timeout)
  - [token (required)](#token-required)
  - [throwError](#throwerror)
  - [requestOptions](#requestoptions)
- [Логирование ошибок](#логирование-ошибок)
  - [Объект ошибки](#объект-ошибки)
  - [Коды ошибок](#коды-ошибок)
    - [ERR_EXPRESS_TVM_INVALID_PROTOCOL](#err_express_tvm_invalid_protocol)
    - [ERR_EXPRESS_TVM_INVALID_TOKEN](#err_express_tvm_invalid_token)
    - [ERR_EXPRESS_TVM_INVALID_SERVER_URL](#err_express_tvm_invalid_server_url)
    - [ERR_EXPRESS_TVM_INVALID_REQUEST](#err_express_tvm_invalid_request)
    - [ERR_EXPRESS_TVM_REQUEST_ERROR](#err_express_tvm_request_error)
    - [ERR_EXPRESS_TVM_TICKETS_ERROR](#err_express_tvm_tickets_error)
- [Полезные ссылки](#полезные-ссылки)

## Установка

```sh
npm install --save @yandex-int/express-tvm --registry=https://npm.yandex-team.ru
```

## Подключение локально

Пример подключения для получения тикетов к _тестовому_ [Чёрному Ящику](https://doc.yandex-team.ru/blackbox) через локальный [TVM-демон](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/).

В первую очередь [заводим приложение](https://wiki.yandex-team.ru/toolbox/project-stub/how-to-start/#3.zavodimprilozhenievtvm) и [заказываем гранты](https://wiki.yandex-team.ru/toolbox/project-stub/how-to-start/#4.zakazyvaemgrantydljalokalnojjrazrabotki) для локальной разработки.

Далее устанавливаем tvmtool-bin (версию старше **1.1.5**):

```sh
npm install --global tvmtool-bin --registry=https://npm.yandex-team.ru
```

Запускаем его, указав порт и токен:

```sh
tvmtool --port 8001 --auth tvmtool-development-access-token
```

Добавляем файл настроек `.tmv.json`:

```
{
  "BbEnvType": 1,
  "clients": {
      "commentator": {
          "secret": "<секрет вашего приложения>",
          "self_tvm_id": <id вашего приложения>,
          "dsts": {
              "blackbox": {
                "dst_id": 224
              }
          }
      },
      "avatarsClient": {
          "secret": "<секрет вашего приложения>",
          "self_tvm_id": <id вашего приложения>,
          "dsts": {
              "avatars": {
                "dst_id": 223322
              }
          }
      }
  }
}
```

Далее используем express-tvm для обращения к TVM-демону
и получаем список [тикетов](./src/interfaces/ticket.d.ts) или [ошибку](./src/interfaces/error.d.ts).

```ts
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

const app = express();

app.use(expressTvmMiddleware({
    // clientId мы определили в .tvm.json
    clientId: 'commentator',
    // Допустимые destinations для clientId мы определили в .tvm.json
    destinations: ['blackbox'],
    // Server URL HTTP API локально запущеного TVM-демона (передавали через --port)
    serverUrl: 'http://localhost:8001',
    // Токен для подключения (передавали через --token)
    token: 'tvmtool-development-access-token'
}));

app.use(expressTvmMiddleware({
    // clientId мы определили в .tvm.json
    clientId: 'avatarsClient',
    // Допустимые destinations для clientId мы определили в .tvm.json
    destinations: ['avatars'],
    // Server URL HTTP API локально запущеного TVM-демона (передавали через --port)
    serverUrl: 'http://localhost:8001',
    // Токен для подключения (передавали через --token)
    token: 'tvmtool-development-access-token'
}));

app.use((req, res, next) => {
    // Смотрим полученные тикеты для каждого clientId отдельно
    console.log(req.tvm && req.tvm.commentator && req.tvm.commentator.tickets);
    // { blackbox:
    //   { ticket: '3:serv:CPIoE...',
    //     tvm_id: 224 } } }

    console.log(req.tvm && req.tvm.avatarsClient && req.tvm.avatarsClient.tickets);
    // { avatars:
    //   { ticket: '3:serv:CPIoE...',
    //     tvm_id: 223322 } } }

    // Или обрабатываем ошибку
    console.error(req.tvm && req.tvm.commentator && req.tvm.commentator.error);

    res.sendStatus(200);
});
```

> :warning: В **JavaScript** подключаем таким образом:

> ```js
> const expressTvmMiddleware = require('@yandex-int/express-tvm').default;
> ```

## Подключение для сервиса в Qloud

Пример подключения для получения тикетов к [Чёрному Ящику](https://doc.yandex-team.ru/blackbox) через [TVM-демон](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/).

В начале [настраиваем конфигурацию](https://wiki.yandex-team.ru/qloud/doc/secrets/TVM/#create-configuration) демона в Qloud.

Далее используем express-tvm для обращения к TVM-демону
и получаем список [тикетов](./src/interfaces/ticket.d.ts) или [ошибку](./src/interfaces/error.d.ts)

```ts
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

const app = express();

app.use(expressTvmMiddleware({
    clientId: 'commentator',
    destinations: ['blackbox'],
    // Server URL HTTP API TVM-демона в Qloud
    // @see https://wiki.yandex-team.ru/qloud/doc/secrets/TVM/
    serverUrl: 'http://localhost:1',
    // Qloud кладёт токен к демону в переменную QLOUD_TVM_TOKEN
    // @see https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#/tvm/tickets
    token: process.env.QLOUD_TVM_TOKEN
}));
```

## Опции

### cacheMaxAge

Type: `number`
Default: `60000`

Кешировать ответ на указанное количество миллисекунд.
Если передать значение `0` – кеширование будет отключено.

Ключ кеша включает в себя **только** [clientId](#clientid-required), [destinations](#destinations-required), [кастомные query-параметры и заголовки](#requestoptions).

### cacheKeyHeaders

Type: `string[]`
Default: `undefined`

По умолчанию, ключ кеша включает в себя все [кастомные заголовки](#requestoptions).

Этой опцией можно ограничить этот набор.

```js
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

express().use(expressTvmMiddleware({
    cacheKeyHeaders: ['X-Cacheable-Custom-Header'],
    clientId: 'commentator',
    destinations: ['blackbox'],
    serverUrl: 'http://localhost:1',
    token: process.env.QLOUD_TVM_TOKEN,
    requestOptions: req => ({
        headers: {
            'X-Custom-Header': '',
            'X-Cacheable-Custom-Header': '',
        }
    })
}));
```

Или убрать заголовки из ключа для кеша, передав пустой массив:

```js
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

express().use(expressTvmMiddleware({
    cacheKeyHeaders: [],
    clientId: 'commentator',
    destinations: ['blackbox'],
    serverUrl: 'http://localhost:1',
    token: process.env.QLOUD_TVM_TOKEN,
    requestOptions: req => ({
        headers: {
            'X-Custom-Header': '',
            'X-Cacheable-Custom-Header': '',
        }
    })
}));
```

### cacheKeyQueryParams

Type: `string[]`
Default: `undefined`

По умолчанию, ключ кеша включает в себя все [кастомные query-параметры](#requestoptions).

Этой опцией можно ограничить этот набор.

```js
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

express().use(expressTvmMiddleware({
    cacheKeyQueryParams: ['cacheableCustomParam'],
    clientId: 'commentator',
    destinations: ['blackbox'],
    serverUrl: 'http://localhost:1',
    token: process.env.QLOUD_TVM_TOKEN,
    requestOptions: req => ({
        query: {
            customParam: '',
            cacheableCustomParam: '',
        }
    })
}));
```

Или убрать заголовки из ключа для кеша, передав пустой массив:

```js
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

express().use(expressTvmMiddleware({
    cacheKeyQueryParams: [],
    clientId: 'commentator',
    destinations: ['blackbox'],
    serverUrl: 'http://localhost:1',
    token: process.env.QLOUD_TVM_TOKEN,
    requestOptions: req => ({
        query: {
            customParam: '',
            cacheableCustomParam: '',
        }
    })
}));
```

### clientId (required)

Type: `string`
Example: `2001019`

Имя или id TVM сервиса, от лица, которого мы запрашиваем тикеты.

### destinations (required)

#### Как массив

Type: `string[]`
Example: `[blackbox, 2001019]`

Спиcок имён или id TVM сервисов, у которых мы запрашиваем тикеты.

Если массив передан пустым, запрос не будет выполенен
и `req.tvm[clientId].tickets` будет заполнен пустым объектом.

#### Как объект

Type: `{ [name: string]: boolean | (req, res): boolean }`
Example:
```js
{
    blackbox: function (req, res) {
        return req && req.cookies && req.cookies.Session_id;
    },
    geobase: true,
    sentry: false
}
```

В качестве **ключа** выступает имя или id TVM сервиса,
в качестве **значения** – _true_, _false_ или функция, которая возвращает _true_ или _false_.

На вход функция принимает объекты [Request](http://expressjs.com/ru/api.html#req) и [Response](http://expressjs.com/ru/api.html#res).

В итоге запрос будет сформирован только к тем TVM сервисам,
для которых указан _true_ или функция, вернувшая _true_.

Если итоговый набор целей будет пустым, запрос не будет выполенен
и `req.tvm[clientId].tickets` будет заполнен пустым объектом.

### serverUrl (required)

Type: `string`
Example: `http://localhost:1`

Базовый URL для HTTP API TVM-демона.

Должен быть **http-only**, в противном случае будет выброшена ошибка [ERR_EXPRESS_TVM_INVALID_PROTOCOL](#ERR_EXPRESS_TVM_INVALID_PROTOCOL).

Должен быть валидным, в противном случае будет выброшена ошибка [ERR_EXPRESS_TVM_INVALID_SERVER_URL](#ERR_EXPRESS_TVM_INVALID_SERVER_URL).

### keepAlive

Type: `boolean`
Default: `true`

Использовать keep-alive в соединении к TVM-демону.

### logger

Type: [ILogger](./src/interfaces/logger.d.ts)

Инстанс внешнего логгера. От интерфейса внешнего логгера ожидается наличие метода `error`, принимающего в качестве первого аргумента ошибку.

### logError

Type: `boolean`
Default: `true`

Логировать ошибку. В противном случае вы может залогировать самостоятельно взяв ошибку из поля `req.tvm[clientId].error`.

### retry

Type: `number`
Default: `1`

Количество перезапросов к TVM-демону.

### timeout

Type: `number`
Default: `100`

Таймаут запроса к TVM-демону в _миллисекундах_.

### token (required)

Type: `string`

Токен для подключения к TVM-демону.

### throwError

Type: `boolean`
Default: `false`

Бросать ошибку. По умолчанию, миддлвара не бросает ошибку, а складывает её в `req.tvm[clientId].error`. Если включить эту опцию вам необходимо самостоятельно позаботиться об обработке ошибки:

```js
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

const app = express();

app.use(expressTvmMiddleware({
    clientId: 'commentator',
    destinations: ['blackbox'],
    serverUrl: 'http://localhost:1',
    token: process.env.QLOUD_TVM_TOKEN
}));

app.use((err, req, res, next) => {
    console.error(err);

    res.sendStatus(500);
});
```

### requestOptions

Type: `object | function`
Default: `undefined`

Способ передать в `got` любые дополнительные параметры.

Можно передать объект, если опции статичны:

```js
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

const app = express();

app.use(expressTvmMiddleware({
    clientId: 'commentator',
    destinations: ['blackbox'],
    serverUrl: 'http://localhost:1',
    token: process.env.QLOUD_TVM_TOKEN,
    requestOptions: {
        headers: {
            'X-Some-Header': '42'
        },
        query: {
            some_key: '42'
        }
    }
}));
```

Или можно передать метод от `req`/`res`, если параметры зависят от запроса.

```js
import express from 'express';
import expressTvmMiddleware from '@yandex-int/express-tvm';

const app = express();

app.use(expressTvmMiddleware({
    clientId: 'commentator',
    destinations: ['blackbox'],
    serverUrl: 'http://localhost:1',
    token: process.env.QLOUD_TVM_TOKEN,
    requestOptions(req) {
        return {
            headers: {
                'X-Some-Header': '42'
            },
            query: {
                some_key: req.query.some_key
            }
        };
    }
}));
```

## Логирование ошибок

По умолчанию, мидлвара логирует ошибки, используя интерфейс `console`.

Параметром [logger](#logger) можно передать свой инстанс логгера. От его интерфейса ожидается наличие метода `error`, принимающего в качестве первого аргумента ошибку.

Если в объекте запроса, в поле `req.logger` уже находится инстанс логгера, то ему будет отдано предпочтение.

Полностью отключить логирование можно опцией [logError](#logerror).

### Объект ошибки

Объект ошибки содержит следующие поля:

* `name` – во всех случаях _ExpressTvmError_
* `massage` – текст ошибки
* `code` – код ошибки, один из [ниже перечисленых](#Коды-ошибок)
* `stack` – стек вызовов, включающий стек `originalError`
* `originalError` – оригинальная ошибка на основе которой сформирована _ExpressTvmError_

### Коды ошибок

#### ERR_EXPRESS_TVM_INVALID_PROTOCOL

Невалидный протокол для обращения к TVM-демону. Поддерживается только **http**.

#### ERR_EXPRESS_TVM_INVALID_TOKEN

Невалидный токен для обращения к TVM-демону.

#### ERR_EXPRESS_TVM_INVALID_SERVER_URL

Невалидный базовый URL для обращения к TVM-демону.

#### ERR_EXPRESS_TVM_INVALID_REQUEST

Невалидный запрос к TVM-демону. Например, указан неверный `destination`.

Пример такой ошибки:
```
http://localhost:8001/tvm/tickets?dsts=muahaha is invalid URL because of
"can't find destination tvmid for src = 2001019, dstparam = muahaha (strconv)"
```

#### ERR_EXPRESS_TVM_REQUEST_ERROR

Ошибка запроса к TVM-демону. Например, он не доступен или запрос не уложилися в обозначенный [timeout](#timeout).

#### ERR_EXPRESS_TVM_TICKETS_ERROR

Ошибка получения одного или нескольких тикетов.

Пример такой ошибки:
```
Failed to get tickets: muahaha(100500) because of "Dst is not found: it never existed.
Or it was created a moment ago and tvm-api needs couple minutes to get it.
client_id=100500"
```

## Полезные ссылки

* [Про TVM-демон](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/)
* [Про настройку TVM в Qloud](https://wiki.yandex-team.ru/qloud/doc/secrets/TVM/)
* Как [завести TVM приложение](https://wiki.yandex-team.ru/toolbox/project-stub/how-to-start/#3.zavodimprilozhenievtvm) и [заказать гранты](https://wiki.yandex-team.ru/toolbox/project-stub/how-to-start/#4.zakazyvaemgrantydljalokalnojjrazrabotki) для локальной разработки
