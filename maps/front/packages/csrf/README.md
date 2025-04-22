# csrf [![build status](https://badger.yandex-team.ru/github/maps/csrf/master/state.svg)](https://a.yandex-team.ru/arc/trunk/arcadia/maps/front/packages/csrf)

Node.js module for generating and checking `csrf` tokens
https://wiki.yandex-team.ru/security/For/developers/csrf-token

## Installation

```
npm install --registry https://npm.yandex-team.ru @yandex-int/csrf
```

## Usage

```js
const {Csrf} = require('@yandex-int/csrf');

const csrf = new Csrf({key: 'CSRF_KEY_FROM_CONFIG'});
const options = {yandexuid: 'yandexuid_cookie_value'};
const token = csrf.generateToken(options);
const isValid = csrf.isTokenValid(token, options);
```

### `xscript`-compliant token

Some services use
[xscript](http://doc.yandex-team.ru/XScript5/interface-developer-guide/concepts/about.xml). To
generate a token for those services function `generateXscriptToken` should be used:

```js
const {generateXscriptToken} = require('@yandex-int/csrf');

const options = {yandexuid: 'yandexuid_cookie_value'};
const token = generateXscriptToken(options);
```

*Note:* this module hasn't way to check generated token.

## Run tests

```
npm install
npm test
```
