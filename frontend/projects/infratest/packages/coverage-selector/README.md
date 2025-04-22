# coverage-selector

Инструмент для построения и использования лога селективности на основе информации о покрытии.

## Установка

```sh
npm install @yandex-int/coverage-selector --registry https://npm.yandex-team.ru
```

## Использование

Использование `coverage-selector` подразумевает две фазы:

1) сбор покрытия и создание лога селективности,
2) использование лога селективности.

### Сбор покрытия

```js
const {Collector, Storage} = require('@yandex-int/coverage-selector');

const storage = new Storage('path/to/log.db');
storage.setup();

const collector = new Collector({storage});
// `coverage` в формате `[{path, startLine, endLine}]`.
await collector.collect(testId, coverage);
```

### Выборка тестов

```js
const {Selector, Storage} = require('@yandex-int/coverage-selector');

const storage = new Storage('path/to/log.db');
const selector = new Selector({storage});

await selector.select(path, [[0, 5], [7, 13]]);
// => ['testId1', 'testId2', ...]
```
