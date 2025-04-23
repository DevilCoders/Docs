# Perf tool

Средство для запуска бенчмарков, может применяться для оценки быстродействия блока

вызов 

```
tools/perf path/to/benchmark.perf-test.js [num-runs|100000] [printJson]
```

в настоящий момент поддерживается только возможность запуска для фичей, раскатанных в коде

## block-name.perf-test.js

Файл с описанием теста, содержит объект, представляющий методы для загрузки скриптов, подготовки входных данных и непосредственно вызова тестируемого блока

```javascript
module.exports = {
    /**
     * Импортирует необходимые для работы бенчмарка файлы
     */
    loadPrivBlocks: function() {
        require('../../../blocks-common/adapter/adapter.priv');
        require('../../../blocks-common/adapter-videowiz/adapter-videowiz.priv');
    },

    /**
     * Задает контекст для запусков
     */
    context: function(context) {
        context.query = {
            uriEscaped: 'aaa'
        };
    },

    /**
     * Переопределяет глобальный контекст (опционально)
     */
    requestCtx: function(RequestCtx) {
        RequestCtx.GlobalContext = RequestCtx.GlobalContext || {};
        RequestCtx.GlobalContext.device = {};
    },

    /**
     * Функция для получения входных данных. Возвращает второй и последующие аргументы для вызова блока
     * 
     * @returns Object[]
     */
    data: function() {
        const docPath = './perf-data/adapter-videowiz_type_vital';

        const doc = require(docPath);

        const docOut = doc;
        const snippet = doc.construct[0];

        return [snippet, doc];
    },

    /**
     * Непосредственно выполнение кода блока. Возвращаемое значение может выводиться при указании
     * соответствующего флага вызова бенчмарка
     *
     * @returns Object
     */
    test: function(args) {
        return blocks['adapter-videowiz_type_vital'](...args);
    }
};
```
