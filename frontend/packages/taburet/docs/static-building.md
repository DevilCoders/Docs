## Сборка статики
Сборка статики настраивается через конфиги webpack.
В конфиге могут использоваться плагины:
- [MultiPlugin](../src-js/webpack/plugins/MultiPlugin/MultiPlugin.md)
- [AssetsJsonPlugin](../src-js/webpack/plugins/AssetsJsonPlugin/AssetsJsonPlugin.md) <- обязателен для работы табурета
- [MainChunkPlugin](../src-js/webpack/plugins/MainChunkPlugin/MainChunkPlugin.md)

В качестве "entry" используются рутовые компоненты фичей, например "src/features/Foo/Foo.entries/desktop.tsx".

Пример конфига с аннотацией настроек описан в пункте [Пример конфига webpack](#пример-"production"-конфига-webpack).

### Основные этапы сборки статики
#### Модификация entry поинтов
В начале необходимо модифицировать enty поинты для конфига webpack. Это нужно для нормальной работы [MultiPlugin](../src-js/webpack/plugins/MultiPlugin/MultiPlugin.md), и делается через вспомогательный метод `patchEntriesWithI18n` из утилиты [i18n](../src-js/webpack/i18n/i18n.md).

#### Генерация main-chunk
Во время компиляции [MainChunkPlugin](../src-js/webpack/plugins/MainChunkPlugin/MainChunkPlugin.md) выделяет наиболее часто используемые модули в отдельный чанк, чтобы не доставлять один и тот же код с разными фичами.

#### Сборка переводов
Следом запускается [MultiPlugin](../src-js/webpack/plugins/MultiPlugin/MultiPlugin.md), который [копирует каждую фичу и подменяет языки](../src-js/webpack/plugins/MultiPlugin/MultiPlugin.md#схема-работы). Это нужно чтобы webpack для каждого "entry" собирал не один чанк `desktop.tsx → [ru.ts, en.ts, ...]`, в котором подключены переводы на все языки, а для каждого языка строил отдельный (`desktop.tsx → desktop.ru.ts, desktop.en.ts` и т.д.).

#### Генерация ассетов
В "prod" режиме webpack может собирать несколько групп чанков ([см. optimization.splitChunks](https://webpack.js.org/plugins/split-chunks-plugin/)). Например, можно разбивать по группам с одинаковым типом модулей:
1. Собственные модули фичи (обычно это все, что лежит в "src/features/Foo/*")
2. Библиотечные модули из "node_modules" и "src/lib"
3. Общие компоненты для фич ("src/components")
4. Асинхронные компоненты

Тогда в конце работы webpack-а [AssetsJsonPlugin](../src-js/webpack/plugins/AssetsJsonPlugin/AssetsJsonPlugin.md) строит `.build/assets/assets.json` со всеми чанками и списком чанков для каждого entry:
```js
{
    // чанк с наиболее часто используемыми модулями сформированный MainChunkPlugin
    "main": "path/to/main-chunk.js",
    "entries": {
        "features/Foo/Foo@desktop": {
            // основной чанк с модулями, используемыми только в этой фиче
            "main": {
                "ru": 10, // номер основного чанка, переведённый на "ru"
                "en": 24, // номер основного чанка, переведённый на "en"
            },
            // номера общих чанков, используемых одной и тойже фичёй с разными локализациями
            "chunks": [ 0, 5, 9... ],
        },
    },
    // все чанки с модулями, которые используются в разных фичах
    "chunks": [
        // 0-ой чанк
        // ассеты, из которых состоит 0-ой чанк (кроме асинхронных)
        [ { "chunk.0.0", "css": "css стили" }, { "chunk.0.1", js: "скрипты" } ],
        // 1-й чанк
        // ассеты, из которых состоит 1-й чанк (кроме асинхронных)
        [ { "chunk.1.0", js { url: "/path/to/js/feature" }, ]
        // 2-й...
    ],
    "componentsExperiments": {
        "components-experiments/flag/desktop": [/* номера чанков, используемых в эксперименте */],
    }
}
```
Все виды чанков, кроме асинхронных, попадают в массив `chunks` в виде различных js/css ассетов:
- Стили нужно сразу подставлять в html целиком (чтобы верстка не моргала), поэтому их ассеты выглядят как `{ name, css: 'стили' }`
- Основные чанки фичей приезжают отдельными ресурсами (чтобы не раздувать html), поэтому их ассеты выглядят как `{ name, js { url: '/path/to/js/feature' } }`
- Библиотечные модули и общие компоненты должны быть доступны из любой фичи, поэтому грузим их подстановкой в html с помощью ассетов вида `{ name, js: 'скрипты' }`

Cтатика, которая доставляется как отдельный ресурс (основные и асинхронные чанки), фризится скриптом из [AssetsJsonPlugin](../src-js/webpack/plugins/AssetsJsonPlugin/AssetsJsonPlugin.md). В общих чертах фризинг представляет из себя простое копирование файлов с хешированием имён по содержимому.

Полученные ассеты [подключаются](./quick-start.md#используем-рантайм-для-подключения–адаптеров-в-приложении) в `Runtime`.

##### Асинхронные модули
Асинхронные модули подключаются динамическим import-ами. При этом асинхронный модуль не запрещается подключать обычным импортом в других местах проекта (в этом случае модуль попадет в два чанка - в синхронный и асинхронный).

__NB:__ Асинхронные чанки фризятся переносом в папку "freeze" с сохранением относительного пути. Например, ".build/static/chunks/f1d5.js" переносится как "freeze/static/chunks/f1d5.js". Делается это, потому что webpack сам обрабатывает динамические import-ы, запоминая пути по которым собиралась статика в качестве url-ов для загрузки статики в рантайме. Если динамических модулей нет, фризинг необязателен.

### Пример "Production" конфига webpack
```js
langs = ['ru', 'en']; // используемые языки
const { entry, output } = config;

module.exports = {
    mode: 'production',
    // добавляет все локализации в список entry
    entry: patchEntriesWithI18n(entry, 'prod'),
    output,
    module: {
        rules: [
            // описываем по каким правилам собирать модули
        ],
    },
    plugins: [
        // Клонирует чанки и подменяет в копиях локализованный контент
        new MultiPlugin({
            // В готовом виде эти настройки можно получить вызвав функцию хелпер getMultiplierConfig из пакета мультиплагина, передав в неё массив с языками.
            replaceSourceMatcher: /\.i18n\/index.js/,
            disconnectMatcher: /\.i18n\/((?!index).)*.js/,
            simpleReplaceMatcher: /config\/i18n\/i18n.prod.js/,
            multi: [{
                isDefaultChunk: true,
                nameSuffix: '.ru',
                replaceModule: [ `export * from './ru';`, 'ru', './ru' ],
                disconnectModulesExcept: 'ru.js',
                simpleReplace: ['I18N_LANG', 'ru']
            },
            {
                isDefaultChunk: false,
                nameSuffix: '.en',
                replaceModule: [ `export * from './en';`, 'en', './en' ],
                disconnectModulesExcept: 'en.js',
                simpleReplace: ['I18N_LANG', 'en']
            }]
        }),
        // Извлекает общие зависимости в отдельный чанк
        new MainChunkPlugin({
            minUsers = 10,
        }),
        // Генерирует файл assets.json для Runtime табурета
        new AssetsJsonPlugin({
            output: './assets.json',
            langs,
            freeze: {
                asyncChunkGroupName: 'async', // должно совпадать с splitChunks.cacheGroups с асинхронными чанками
                enabled: true,
                path: 'freeze',
            },
        }),
    ],
    optimization: {
        splitChunks: {
            cacheGroups: {
                // пишем нужные группы разбиения по чанкам

                // асинхронные чанки выделяем в отдельную группу
                async: { // название должно совпадать с freeze.asyncChunkGroupName
                    enforce: true,
                    chunks: 'async',
                },
            }
        },
    }
};
```

### "Dev" сборка
В "dev" режиме webpack не обязательно использовать плагины или дробить бандлы. Для каждого "entry" можно собирать собственные бандлы, и не делать отдельные чанки для стилей или часто используемых модулей.
