# ya-notify-client
[![](https://drone.yandex-team.ru/api/badges/toolbox/ya-notify-client/status.svg)](https://drone.yandex-team.ru/toolbox/express-tvm)
![](https://badger.yandex-team.ru/npm/@yandex-int/ya-notify-client/version.svg)
![](https://badger.yandex-team.ru/npm/@yandex-int/ya-notify-client/owner.svg)

Клиент для API [`ya notify`](https://wiki.yandex-team.ru/yatool/notify), который умеет отправлять сообщения
в Telegram от имени `@YaNotifyBot`.

- [Установка](#Установка)
- [Использование](#Использование)
- [Опции](#Опции)
    - [endpoint (required)](#endpoint-required)
    - [token (required)](#token-required)
    - [gotOptions](#gotoptions)

## Установка

```sh
npm install --save @yandex-int/ya-notify-client --registry=https://npm.yandex-team.ru
```

## Использование

```js
const YaNotifyClient = require('@yandex-int/ya-notify-client');

const yaNotifyClient = new YaNotifyClient({
    endpoint: 'http://api-yanotifybot.n.yandex-team.ru',
    token: '<token>'
});

(async () => {
    try {
        const body = await yaNotifyClient.sendMessage({
            message: 'Hi!',
            users: ['savichev'],
            parseMode: 'HTML'
        });

        console.info(body);
        //=> 'Message send to savichev@.'
    } catch (err) {
        console.error(err);
        //=> got.HTTPError
    }
})();
```

## Опции

### endpoint (required)

Type: `string`<br/>
Example: `http://api-yanotifybot.n.yandex-team.ru`

Базовый URL для HTTP API `ya notify`.

### token (required)

Type: `string`

Токен для авторизации робота, от имени которого будут приходить сообщения в Telegram.

Может подойти любой [токен](https://wiki.yandex-team.ru/intranet/dev/oauth/#otimenirobota),
который идентифицирует вашего робота. Например, токен для [API Стаффа](https://wiki.yandex-team.ru/staff/api).

### gotOptions

Опции для модуля [`got`](https://www.npmjs.com/package/got).

По-умолчанию включены опции:
- `agent: new Agent({ keepAlive: true })`
- `json: true`
- `timeout: 5000`
- `retry: 2`
