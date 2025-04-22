# bunker-filter

Процессор, помогающий фильтровать ноды. Испольуется в [bunker-to-js](https://github.yandex-team.ru/project-stub/bunker-to-js).

## Usage

```js
var bunker = require('bunker-to-js');
var filter = require('bunker-filter');

bunker()
    .use(filter.hidden)
    .use(filter.empty);
```

## API

### filter.hidden

Отфильтровывает скрытые ноды или ноды, находящиеся в скрытых папках (начинающихся с `.`).

### filter.empty

Отфильтровывает ноды, у которых нет контента (обычно, такие ноды не проходят по `isDeleted === false`).
