# ts-push-module-cancel

Один из typescript-трансформеров, необходимых для работы механизма PushModule в web4.
Реализует фолбэк на обычные импорты для development-окружения на стороне клиента.

## Разработка

1. Для форматирования кода используется [prettier](https://prettier.io/), поэтому оно немного отличается от общепринятого в монорепе.
   Используйте, пожалуйста, этот инструмент для сохранения единообразного форматирования.
2. Пакет планируется использовать в web4, поэтому, чтобы запускать тесты в том же окружении, в котором пакет будет применяться,
   версия typescript установлена такая же, как в web4. Она отличается от принятной в монорепе, поэтому пакет пришлось внести в
   [список исключений depslint](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.depslint.json). Поэтому при добавлении
   новых зависимостей нужно вручную следить за соблюдением [правил монорепы](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/requirements.md#требования-к-зависимостям-npm-пакетов-2).
3. У пакета 100% тестовое покрытие. Следите за тем, чтобы оно не уменьшалось. Чтобы посмотреть на объем тестового покрытия, достаточно
   запустить команду `npm run test:coverage` (перед этим убедитесь, что у вас собрана свежая версия пакета:
   `npm install && npm run build`).

## Использование

```js
// webpack.config.js
const transformer = require('ts-push-module-cancel');

const config = {
    loader: require.resolve('ts-loader'),
    options: {
        // ...
        getCustomTransformers: process.env.NODE_ENV === 'development' && () => ({
            before: [transformer],
        }),
    },
};
```

## Что трансформер делает

Заменяет пушмодуль-импорты на обычные.
Пушмодуль-импорт – это выражение вида `PushModuleRenderer.pushModuleRendererImport(import('path/to/Component'))`.

Например:

```js
// Было
new Registry().fill({
    registryComponent: obj.pushModuleRendererImport(import('path/to/Component')),
});

// Стало
new Registry().fill({
    registryComponent: __webpack_require__(require.resolve('path/to/Component')).default,
});
```

### Что за `__webpack_require__`?

Результирующий код с точки зрения webpack эквивалентен такому:

```js
import Component from 'path/to/Component';

new Registry().fill({
    registryComponent: Component,
});
```

Однако вариант с `__webpack_require__` обходится одним выражением вместо двух, поэтому он проще с точки зрения трансформации.
