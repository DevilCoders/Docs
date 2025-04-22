## apphost-adapter

Адаптер на время перехода с http на apphost-адаптер РР.

* `apphost-adapter.priv.js` — основной метод адаптера, вызывается в sakhalin/blocks-common/i-global/i-global.priv.js
* `./__context-parser/` — метод для переноса данных из аппхостового контекста в data по заданной схеме
* `./__schemes/` — схемы сервисов с описанием правил переноса данных из аппхостового контекста
* `./__transformers/` — методы для преобразования данных из аппхостового контекста к старому виду

### Формат схемы
```js
module.exports = {
    type: {
        __path: 'path.in.data',
        field1: {
            __path: 'path.in.data',
            subfield1: {
                __path: 'path.in.data',
                __transform: function(ctx, { path, data, reportData }) {
                    return String(data);
                }
            },
            subfield2: {
                __path: ['path.in.data', 'and.other.path'],
                __transform: function(ctx, { path, data, reportData }) {
                    if (path === 'and.other.path') {
                        return Number(data);
                    }

                    return data;
                }
            }
        }
    }
};
```

### Пример метода transform:
```js
/**
 * Преобразует объект restrictions
 * @param {Object} ctx
 * @param {Object} data
 * @param {String} path
 * @param {GlobalData} reportData
 * @returns {Object[]}
 */
module.exports = function(ctx, { data, path, reportData }) {
    if (path !== 'restrictions') {
        // На случай, если в аппхостовый контекст не приходят какие-то данные и их
        // невозможно вычислить по имеющимся, можно зафоллбэчить на репортовые данные
        return reportData.restrictionsByName;
    }

    // Преобразуем к массиву
    return Object.keys(data).reduce((acc, val) => {
        acc.push(data[val]);
        return acc;
    }, []);
};
```
