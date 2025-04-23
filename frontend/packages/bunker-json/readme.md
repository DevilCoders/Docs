# bunker-json

Парсер JSON содержимого ноды из Бункера. Испольуется в [bunker-to-js](https://github.yandex-team.ru/project-stub/bunker-to-js).

Матчится на все ноды с mime-типом `application/json`.

## Usage

```js
var bunker = require('bunker-to-js');
bunker().parse(require('bunker-json'));
```

## API

### bunker-json

Функция парсер, которая запишет результат `JSON.parse` от запрошенного содержимого ноды.
