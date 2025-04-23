# ginny/no-page-object-service-locator

Запрещает ginny PO service locator

## Примеры

Примеры **неправильного** кода:

```js
this.createStories('n-block');
```

Примеры **правильного** кода:

```js
const Block = require('./n-block');

this.createStories(Block);
```

[*Остальные примеры смотрите в тестах.*](../../../tests/lib/rules/ginny/no-page-object-service-locator.js)