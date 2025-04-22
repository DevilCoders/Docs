# ticount-avg-traces
Пакет для получения трейсов, соответствующих средним метрикам из отчета `ticount`.
Подключается через систему плагинов.

Пакет экспортирует функцию, результат вызова которой 3 плагина:
## storeTracePlugin
Плагин для сохранения связи между сырым трейсом из Chromium и распарсенными метриками через `ticount`.
Используется внутри хука `afterPageOpening`.

## saveTracesToFilePlugin
Плагин для записи в файл результатов выполнения `storeTracePlugin`. Используется внутри хука `afterShooting`.
В качестве параметров принимает объект с полем `filePath` - путь до файла с рассширением `.json`, куда записывать результат.

## findAvgTracesPlugin
Плагин для поиска трейсов, соответствующих средним метрикам. Используется внутри хука `afterAggregation`.
В качестве параметров принимает путь до файлов c базовыми (`baseTracesFile`) и целевыми (`actualTracesFile`) метриками.
Файлы должны быть сохранены плагином `saveTracesToFilePlugin`. Результат вычислений - три файла: 2 файла сырых трейсов Chromium и
html файл с отчетом. При открытии отчета происходит редирект на `https://chromedevtools.github.io/timeline-viewer`.

## Пример использования
Выполняем обстрел целевой и базовой страниц:
```js
// ticount.shooting.config.js
const createAvgTracesPlugins = require('@yandex-int/ticount-avg-traces');

const { saveTracesToFilePlugin, storeTracePlugin } = createAvgTracesPlugins();

module.exports = {
    plugins: {
        afterPageOpening: [[storeTracePlugin]],
        afterShooting: [[saveTracesToFilePlugin, { filePath: process.env.TICOUNT_DATA_FILE }]],
    }
};
```
```bash
TICOUNT_DATA_FILE="base.json" npx ticount write --url=<base-url> --config=ticount.shooting.config.js
TICOUNT_DATA_FILE="actual.json" npx ticount write --url=<actual-url> --config=ticount.shooting.config.js
```

Выполняем агрегацию:
```js
// ticount.compare.config.js
const createAvgTracesPlugins = require('@yandex-int/ticount-avg-traces');

const { findAvgTracesPlugin } = createAvgTracesPlugins();

module.exports = {
    plugins: {
        afterAggregation: [
            [
                findAvgTracesPlugin,
                {
                    actualTracesFile: process.env.TICOUNT_ACTUAL_DATA_FILE,
                    baseTracesFile: process.env.TICOUNT_BASE_DATA_FILE,
                    reportDir: process.env.TICOUNT_REPORT_DIR
                }
            ]
        ]
    }
};
```
```bash
TICOUNT_BASE_DATA_FILE="base.json" \
TICOUNT_ACTUAL_DATA_FILE="actual.json" \
TICOUNT_REPORT_DIR="report/" \
npx ticount compare --skip-shooting --config=ticount.compare.config.js
```
