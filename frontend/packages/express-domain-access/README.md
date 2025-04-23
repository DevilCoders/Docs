# express-domain-access [![Build Status](http://drone-beta.haze.yandex.net/api/badges/project-stub/express-domain-access/status.svg)](http://drone-beta.haze.yandex.net/project-stub/express-domain-access)


Отключение нежелательных доменов для страницы.

## Usage

```js
const express = require('express');
const expressTld = require('express-tld');
const expressDomainAccess = require('express-domain-access');

const app = express();

app.use(expressTld());
app.use(expressDomainAccess('ru,com'));
```

## API

### expressDomainAccess(allowedDomains)

Возвращает миддлвару.

#### allowedDomains

_Тип_: `String`, `Array`

Список разрешенных доменов. Может быть массивом доменов или списком доменов, разделенных через `,`.

## License

MIT
