# ginny/no-page-object-get

Запрещает использовать PageObject.get

## Примеры

Примеры **неправильного** кода:

```js
const {PageObject} = require('ginny');

const Button = PageObject.get('button');
```

Примеры **правильного** кода:

```js
const Button = require('@/spec/page-objects/button');
```