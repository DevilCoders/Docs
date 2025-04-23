# express-tld [![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/express-tld/status.svg)](https://drone.yandex-team.ru/project-stub/express-tld)

Top level domain parser.

## Usage

```js
var express = require('express');
var app = express();

var expressTld = require('express-tld');

app.use(expressTld());

app.get(function(req, res) {
	res.send('Top level domain: ' + req.tld);
});
```

## Examples

| Input             | Output    |
| ----------------- | --------- |
| yandex.ru         | ru        |
| yandex.net        | net       |
| yandex.com.tr     | com.tr    |
| yandex.google.ru  | ru        |
| localhost         | localhost |
| 127.0.0.1         | undefined |

## API

### expressTld()

Returns middleware.
