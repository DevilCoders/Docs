# express-yandexuid [![Build Status](http://drone-beta.haze.yandex.net/api/badges/project-stub/express-yandexuid/status.svg)](http://drone-beta.haze.yandex.net/project-stub/express-yandexuid)

Мидлвара выставляющая куку yandexuid для яндексовых доменов.

 * https://wiki.yandex-team.ru/Cookies/yandexuid – Описание формата и назначения куки yandexuid

### Миграция на v3

Для корректной работы требуется подключение мидделвары express-uatraits вместо express-tld.

### Миграция на v2

Для корректной работы требуется подключение мидделвары [express-tld](https://github.yandex-team.ru/project-stub/express-tld).
После этого миддлвара будет делать `Redirect` на `pass.yandex.tld` (согласно [документации](https://wiki.yandex-team.ru/passport/mda/intro/#kakosushhestvljaetsjakopirovaniekukizdomenavdomen)).

## Install

```
npm install --registry http://npm.yandex-team.ru express-yandexuid
```

## Usage

```js
var app = express();

app.use(require('express-yandexuid')());

app.get('/', function (req) {
	console.log(req.cookies.yandexuid);
});
```

## API

### express-yandexuid([options])

## Options

#### yaDomain
Type: `String`
Default: `.yandex.{tld}` (`{tld}` — текущий домен)

Домен, на котором устанавливается кука.
Например: `.kinopoisk.ru`

#### expires
Type: `Date`
Default: `expires.setFullYear(expires.getFullYear() + 10)`

Срок жизни куки.

## Running tests

```
npm run lint
npm test
```
