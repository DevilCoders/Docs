# bunker-cache

Простой кеш `node.content` в памяти. Испольуется в [bunker-to-js](https://github.yandex-team.ru/project-stub/bunker-to-js).

## Usage

```js
var bunker = require('bunker-to-js');
var cache = require('bunker-cache');

bunker()
    .use(cache());
```

## API

### cache()

Возвращает кеширующий процессор нод. Подменяет содержимое ноды, если оно было закешировано.
