# express-uatraits-mock [![Build Status](http://drone.haze.yandex.net/api/badge/github.yandex-team.ru/project-stub/express-uatraits-mock/status.svg?branch=master)](http://drone.haze.yandex.net/github.yandex-team.ru/project-stub/express-uatraits-mock)

Usage:

```js
var express = require('express');
var uatraits = require('express-uatraits-mock');

var app = express()
    .use(uatraits());
```

## API

### uatraits([override])

Создает в `req` свойство `uatraits` с полем `isBrowser: true` и дополняет полями из `override`.
