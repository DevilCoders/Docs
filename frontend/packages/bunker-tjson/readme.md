# bunker-tjson

Парсер [TJSON](https://github.yandex-team.ru/project-stub/tjson) содержимого ноды из Бункера. Испольуется в [bunker-to-js](https://github.yandex-team.ru/project-stub/bunker-to-js).

Матчится на все ноды с mime-типом `application/json; schema="bunker:/.schema/tjson#"`.

## Usage

```js
var bunker = require('bunker-to-js');
bunker().parse(require('bunker-tjson'));
```

## API

### bunker-tjson

Функция парсер, которая запишет результат `new TJSON(JSON.parse(content))` от запрошенного содержимого ноды.

API для TJSON описано в репозитории модуля [tjson](https://github.yandex-team.ru/project-stub/tjson).
