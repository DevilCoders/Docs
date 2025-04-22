# Ticount

Инструмент для сбора и сравнения количества процессорных инструкций.

## Запуск
- Проверка работоспособности инструмента
```bash
ticount test
```
- Сбор метрик для конкретной страницы
```bash
ticount write --url <url> --metrics-log <metrics-log>
```
- Сравнение метрик для двух страниц 
```bash
ticount [compare] --url-base <url-base> --url-actual <url-actual> [--repeat <N>] [--mobile]
```

Для более подробной информации о запуске можно запустить хелп:
```bash
ticount [test|write|compare] --help
```

## Конфигурация
Для поиска файла конфигурации используется пакет `cosmiconfig`. Название модуля - `ticount`.
Способы задания конфигурации:
- свойство `ticount` в `package.json` вашего модуля;
- `.ticountrc` файл в JSON или YAML формате;
- `.ticountrc.json`, `.ticountrc.yaml`, `.ticountrc.yml`, `.ticountrc.js`, или `.ticountrc.cjs` файл;
- `ticount.config.js` или `ticount.config.cjs`;
- при запуске команды можно указать путь до конфига:
```bash
ticount write --config <path-to-config> --url <url>
```

```js
// Пример конфига ticount.config.js

module.exports = {
    shootingTimeout: 30000, // время ожидания загрузки целевой страницы
    exitOnError: false, // завершить процесс с кодом "1" при падении одной из задач
    // опции запуска воркеров
    clusterOptions: {
        repeat: 100, // количество задач (сколько раз будет открыта страница для сбора метрик)
        workers: 10, // количество воркеров
        retry: 0, // количество повторных запусков задачи при падении
    },
    // опции запуска puppeteer.launch
    puppeteerOptions: {
        ignoreHTTPSErrors: true,
        args: ['--no-sandbox', '--enable-thread-instruction-count'],
    },
    // плагины
    plugins: {
        beforePageOpening: [
            [async ({ timeout }, { page }) => await page.goto('https://ya.ru', { timeout }), { timeout: process.env.TIMEOUT }],
            ['@yandex-int/ticount-some-plugin', { foo: 'bar' }],
        ]
    },
    // дополнительный набор метрик, для которых будет рассчитана агрегация и которые попадут в отчет
    metrics: {
        // <название timeMark из rum>: <название метрики в отчете ticount>
        '3036': 'js_framework_inited'
    }
};
```

## Система плагинов
До сбора метрик производительности и после их сбора можно выполнить произвольный код, используя систему плагинов.
Плагины можно подключить через конфигурационный файл, в свойстве `plugins`:
```js
const config = {
    plugins: {
        // плагины, выполняющиеся перед обстрелом страниц
        beforeShooting: [],
        // плагины, выполняющиеся до сбора метрик
        beforePageOpening: [],
        // плагины, выполняющиеся перед остановкой трейса
        beforeTracingStop: [],
        // плагины, выполняющиеся после сбора метрик
        afterPageOpening: [],
        // плагины, выполняющиеся после обстрела страниц
        afterShooting: [],
        // плагины, выполняющиеся после аггрегации метрик
        afterAggregation: [],
    }
}
```

Плагин может быть как функцией, так и npm модулем. Сигнатура выглядит следующим образом:
```ts
type TicountPlugin = (options: unknown | undefined, context: PluginContext) => Promise<void> | void;
```
Здесь `options` - параметры плагина, которые передаются через конфиг, `context` - контекст исполнения, который зависит от
места вызова плагина:

### Контексты исполнения
```ts
type BeforeShootingContext = undefined;
type BeforePageOpeningContext = {
    page: Page;
}
type BeforeTracingStopContext = {
    page: Page;
}
type AfterPageOpeningContext = {
    page: Page;
    trace: {
        raw: unknown;
        parsed: Record<string, number>;
        filePath?: string;
    };
}
type AfterShootingContext = undefined;
type AfterAggregationContext = {
    result: AggregatorResult;
};
```

### Функция
В конфиге задается как массив из двух значений: первое - непосредственно функция, второе - опции, передаваемые в функцию:
Пример подключения:
```js
const functionPlugin = async ({ timeout }, { page }) => {
    await page.goto('https://ya.ru', { timeout });
};

module.exports = {
    plugins: {
        beforePageOpening: [functionPlugin, { timeout: process.env.TICOUNT_TIMEOUT }]
    }
}
```

### npm модуль
Npm модуль должен экспортировать функцию.
В конфиге задается как массив из двух значений: первое - название пакета, второе - опции, передаваемые в функцию:
```js
// node_modules/ticount-some-plugin/index.js
module.exports = async (options, { page, trace }) => {
    await page.goto('https://ya.ru', options);
};

// ticount.config.js
module.exports = {
    plugins: {
        beforePageOpening: [
            ['ticount-some-plugin', { timeout: process.env.TICOUNT_TIMEOUT }],
        ]
    }
}
```
