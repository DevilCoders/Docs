# ts-push-module-definition

Трансформер, необходимый для работы механизма PushModule в web4.

## Использование

```js
// webpack.config.js
const transformerFactory = require('ts-push-module-definition');

const config = {
    loader: require.resolve('ts-loader'),
    options: {
        // ...
        getCustomTransformers: () => ({
            before: [transformerFactory()]
        })
    }
};
```

## Что трансформер делает

1. Заменяет вызов `webpackSafePushModule(id)`
    ```js
    // Было
    if (webpackSafePushModule(id)) { console.log(`module ${id} loaded`); }

    // Стало
    if (id && __webpack_require__ && __webpack_require__.m && __webpack_require__.m[id]) {
        console.log(`module ${id} loaded`);
    }
    ```

2. Заменяет вызов `obj.pushModuleRendererImport(import(path))`

    ```js
    // Было
    new Registry().fill({
       registryComponent: obj.pushModuleRendererImport(import(path)),
    });

    // Стало
    new Registry().fill({
        registryComponent: obj.pushModuleRenderer({
            id: typeof window === 'object' ?
                require.resolveWeak(path) :
                require.resolve(path),
            client() {
                if (typeof window === 'object') {
                    return import(path);
                }
            },
            server() {
                if (typeof window === 'undefined') {
                    return require(path);
                }
            },
        })
    });
    ```

## Полезные ссылки
- https://github.com/TypeStrong/ts-loader#getcustomtransformers
