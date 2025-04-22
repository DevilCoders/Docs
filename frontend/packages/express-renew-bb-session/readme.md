# express-renew-bb-session [![Build Status](http://drone-beta.haze.yandex.net/api/badges/project-stub/express-renew-bb-session/status.svg)](http://drone-beta.haze.yandex.net/project-stub/express-renew-bb-session)

Обновляет сессионную куку от Черного Ящика при статусе `NEED_RESET`.

Подробнее смотри в ["Сроке жизни авторизационной куки"](https://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/authorization-policy-resign.xml).

## Install

```
$ npm install --save express-renew-bb-session
```

## Usage

```js
const express = require('express');
const expressTld = require('express-tld');
const expressBlackbox = require('express-blackbox');
const expressRenewBbSession = require('express-renew-bb-session');

const app = express();

app.use(expressBlackbox());
app.use(expressTld());
app.use(expressRenewBbSession());
```


## API

### expressRenewBbSession()

Возвращает миддлвару.

## License

MIT © [Vsevolod Strukchinsky](http://staff.yandex-team.ru/floatdrop)
