# apiary/no-context-manipulations

Правило, запрещающее использовать что-либо из контекста напрямую в контроллере виджета

> Почему?

Все манипуляции должны происходить в хелперах и резолверах, на которые написаны юнит тесты

## Примеры

Примеры **неправильного** кода:

```flow js
export default function (ctx: Context, {inner}: Options): * {
    const fooBarPromise = ctx.resource('get.someStuff');
}
```

```flow js
export default function (ctx: Context, {inner}: Options): * {
    const history = ctx.request.cookie['history']
}
```

Примеры **правильного** кода:

```flow js
import {getSomeStuff} from 'resolvers/stuff';
  
export default function (ctx: Context, {inner}: Options): * {
    const fooBarPromise = getSomeStuff(ctx);
}
```

```flow js
import {getHistory} from 'helpers/history';

export default function (ctx: Context, {inner}: Options): * {
    const history = getHistory(ctx);
}
```

## Конфигурация

```js
module.exports = { 
    rules: {
        'market/apiary/no-context-manipulations': [
            'error', // level
            {
                // глоб-пути к файлам контроллеров, обязательный параметр
                files: [
                    '**/path/to/widgets/**/controller.js', 
                    'maybe/other/specific/path',
                ],
                // имя аргумента контекста, по умолчанию "ctx"
                contextArgumentName: ["ctx", "context"],
            },
        ],
    }
};
```