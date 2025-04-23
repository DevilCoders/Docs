[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/tools/webpack)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/tools/webpack) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/webpack)](https://oko.yandex-team.ru/pkg/@yandex-market/webpack)

[![OKO health](https://badger.yandex-team.ru/oko/repo/market/webpack/health.svg)](https://oko.yandex-team.ru/repo/market/webpack)

Общие конфиги вебпака
===================

Здесь присутсвуют фкункции для генерации конифигов 2х типов:
- **browser** для сборки браузерного бандла
- **server** для сборки серверного бандла

Все они принимают почти одинаковый конфиг:

```js
const config = {
  "environment": process.env.NODE_ENV || 'development',
  "repoRoot": process.cwd(),
  "levitanType": "desktop",          // значение для переменной LEVITAN_PLATFORM
  
  "distPath": "dist/browser",        // путь куда собирать всё
  "browserDistPath": "dist/browser", // можно выставить отдельно для браузера
  "serverDistPath": "dist/server",   // и для сервера
  
  "appEntry": "app/index.js", // точка входа для сборки сервера
  "clientEntry": "", // точка входа в клиентское приложение, которая никогда не должна попадать в серверную сборку
  
  "roots": ["src/widget/pages"], // список корней для поиска страниц см. ниже
  "vendorLibs": ["src/utils/initClient/libSharing.js"], // библиотеки которые нужно добавить в vendor, автоматом инициализируются на клиенте
  "entrypoints": {someEntry: ['src/some/entry']}, // ручная настройка/донастройка ентрипоинтов
  "resolversPath": "src/resolvers", // обязательное поле для настройки пути к резолверам
  
  "inlineStyles": false,      // будут ли инлайниться стили. см. ниже
  "browserList": ["> 0.5%"],  // обязательное поле для настройки браузерных бандлов
  "legacyWrappwer": false,    // использовать старый враппер см. ниже
  
  "babelConfig": "babel.config.json",         // конфиг бабеля
  "browserBabelConfig": "babel.browser.json", // отдельно для браузера
  "serverBabelConfig": "babel.server.json",   // и для сервера
  
  "vendorMinChunks": 1,        // значение minChunks для чанка vendor
  
  "vendorTest": /[\\/](node_modules|src)[\\/]/,       // значение test для чанка vendor
  
  "cssIndent": {localIdentName: '[hash:base64:10]'},  // настройка cssLocalIndent. см. ниже
  "cssIndentContextSuffix": context => {
    const platfromSpecific = context.resourcePath
        .split('.')
        .slice(-2)[0];
      
    return (platfromSpecific === 'touch' || platfromSpecific === 'desktop') 
        ? platfromSpecific
        : '';
  },
  "chunkSplitting": {  // настройки чакнсплиттинга. см. ниже
    runtimeChunk: {
      name: 'vendor',
    },
    moduleIds: 'natural',
    splitChunks: {
      cacheGroups: {
        commons: {
          name: 'vendor',
          test: vendorTest,
          minChunks: vendorMinChunks,
          chunks: 'all',
          enforce: true,
        },
      },
    },
  }
}
``` 

### Обязательные поля

Для браузерной сборки:
  - roots / entrypoints (хотя бы одно)
  - resolversPath
  - browserList
  
Для серверной сборки пока нет обязательных полей.

### inlineStyles

Когда стили не выдаются со статического кластера, а встраиваются непосредственно в страницу, все ресурсы на которые они ссылаются, начинают пытаться загрузиться по относительным путям с текущего домена. Домен со статикой определяется в рантайме, так что нельзя просто прописать его при сборке. Для решения этой проблемы ко всем путям добавляется префикс YA_MARKET_STATIC_URL, который в рантайме нужно подменить на путь до статики. В деве проставляется путь /dist/browser - таким образом можно грузить стили как инлайном так и по ссылке.

### cssIndent и cssIndentContextSuffix

Настройка cssIndent позволяет вручую указать как требуется именовать локальные css-селекторы. см. https://webpack.js.org/loaders/css-loader/#localidentname и https://webpack.js.org/loaders/css-loader/#getlocalident

Если параметр cssIndent не указан, то используется скрипт [helpers/css-local-indent.js](lib/helpers/css-local-indent.js), параметр cssIndentContextSuffix будет передан в него последним параметром. В конфиге выше приведён пример как этот метод выглядел бы для Беру.

### roots

Данное поле принимает массив строк или объектов вида

```js
const rootsEntity = {
    root: "some/path", // путь для поиска директорий с файлами index.js
    common: ["array/of/paths"], // набор файлов которые трубется добавить в ентрипоинт
    index: "index.js" // какой файл вместо index.js искать
}
```

строки при этом фактически интерпретируются как `{root: value}`. В результате обработки будут добавлены ентрипоинты с названиями директорий и ссылками на index.js файлы и содержимым поля common. Для любопытствующих - данная логика реализована в файле [helpers/get-entrypoints.js](lib/helpers/get-entrypoints.js)

### legacyWrappwer

Флаг для использования старого формата враппера для браузерной сборки. Подробнее см. в [plugins/wrapper.js](lib/plugins/wrapper.js)

### chunkSplitting
Настройки чанк-сплиттинга. Фактически содержимое поле optimization. По-умолчанию используются настройки из [layers/chunk-splitting.js](lib/layers/chunk-splitting.js)

## Использование

```js
const {browser, server} = require('@yandex-market/webpack');

// берём конфиги по типу того который указан выше
const {serverConfig, apiaryConfig, legacyConfig} = require('./configs.js');

module.exports = [
    browser(apiaryConfig),
    browser(legacyConfig),
    server(serverConfig)
];
```
