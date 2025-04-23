# qloud-api

Простая имплементация [Qloud API](https://wiki.yandex-team.ru/qe/qloud-api/) на JS.

## Пререквизиты

* Node.JS 4+
* [Qloud OAuth token](https://auth-secrets.qloud.yandex-team.ru/users/)

## Установка

```bash
npm install --save git://github.yandex-team.ru/qloud/qloud-api.git
```

или

```bash
npm install --save --registry http://npm.yandex-team.ru qloud-api
```

## Использование

```js
const QLoudAPI = require('@yandex-int/si.ci.qloud-api');
const api = new QLoudAPI({
    host: 'https://qloud.yandex-team.ru',
    token: process.env.QLOUD_OAUTH_TOKEN
});
```

Более подробный пример см. в [`example.js`](example.js).

## Разработка

```bash
git clone https://github.yandex-team.ru/qloud/qloud-api.git
cd qloud-api
npm install
QLOUD_OAUTH_TOKEN=token node example.js
```
