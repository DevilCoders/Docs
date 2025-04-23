# mandrel/require-resolver-name

Правило обязывает разработчика указывать имя для резолвера.

> Зачем?

Имя резолвера попадает в логи, что упрощает их чтение и восприятие

> Зависимости?

Требуется мандрель версии `3.0.5` или выше

## Примеры

Примеры **неправильного** кода

```js

import {createResolver} from '@yandex-market/mandrel/resolver';

export default createResolver((ctx, params) => {/* ... */});
// Имя должно быть непустым
export default createResolver((ctx, params) => {/* ... */}, {name: ''});

```

Примеры **правильного** кода

```js

import {createResolver} from '@yandex-market/mandrel/resolver';

export const resolveSomething = createResolver(
    (ctx, params) => {/* ... */},
    {
        name: 'resolveSomething',
    }
);

export default createResolver(
    function resolveSomethingElse(ctx, params) {/* ... */},
);

```

Ограничение: вынос настроек в отдельную переменную отключает проверку

```js
const settings = {};
export default createResolver(
    (ctx, params) => {/* ... */},
    settings
)
```