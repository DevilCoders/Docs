# webpack-utils

Общие тулзы для работы с `webpack`.

## get-configs

Основная функция. Формирует конфиги для `webpack.config.js`.
Рассчитывает, что серверные входные точки заканчиваются на `server.js`,
а клиенсткие на `client.js`.

Если проект разбит на бандлы, то входные точки должны лежать в подпапках, например:
```
entries
├── add-offer
│   ├── client.js
│   └── server.js
├── banner
│   ├── client.js
│   └── server.js
└── common
    ├── client.js
    └── server.js
```

### Опции

* `{String} folder` - Папка в которой необходимо искать входные
точки для бандлов. **Обязательное поле**.
* `{Object} config` - Конфиг для бандлов. **Обязательное поле**.
* `{Object} configOverride` - Позволяет переопределять конфиг для конкретных бандлов.

### Переменные окружения

* `BUNDLE` - Для какого бандла вернуть конфиг. Можно указать несколько через запятую.
Если не задана, вернуться конфиги для всех бандлов.

Также, поддерживает переменные окружения для функций `get-client-config` и `get-server-config`,
так как они используются под капотом.

### Пример использования

```
entries
├── add-offer
│   ├── client.js
│   └── server.js
├── banner
│   ├── client.js
│   └── server.js
└── common
    ├── client.js
    └── server.js
```

```js
const getConfigs = require('@realty-front/webpack-utils/get-configs');
const config = require('./app/config');

module.exports = getConfigs({
    folder: './entries',
    config: { platform: 'desktop', publicPath: `${config.get('staticPath')}/` },
    configOverride: {
        banner: { platform: 'desktop', publicPath: `/banner-assets/` }
    }
});
```

## get-client-config

Формирует конфиг для клиентского бандла.

### Опции

Все опции не являются обязательными.

* `{String} bundleName` - Имя бандла. Дефолт - `''`
* `{String} bundlePath` - Путь к бандлу. Дефолт - `'./entries/<bundleName>/client.js'`
* `{String} publicPath` - Поле `webpack.output.publicPath`. Дефолт - `'/build/assets/'`
* `{String} hmrPath` - Путь для `webpack hmr`. Дефолт - `'/__webpack_hmr'`
* `{String} clientBuildDir` - Путь куда собирать клиентский код. Дефолт `'./build/assets/'`
* `{String} serverBuildDir` - Путь куда собирать серверный код. Дефолт `'./build/server/'`
* `{String} svgSpriteRuntimeGeneratorPath` - Абсолютный путь до рантайма генератора спрайта.
Дефолт `'@realty-front/webpack-utils/lib/svg-sprite/runtime-generator-ssr.js'`
* `{String} platform` - Для какой платформы собирать. Дефолт - `'desktop'`

### Переменные окружения

* `NODE_ENV` - Окружение. Дефолт - `development`
* `ANALYZE` - Включить BundleAnalyzer
* `DISCARD_CSS` - Не собирать стили
* `DISCARD_IMG` - Не собирать картинки
* `DISCARD_FONTS` - Не собирать шрифты
* `HOT` - Включить `hot reload`

### Пример использования

```js
const getClientConfig = require('@realty-front/webpack-utils/get-client-config');

module.exports = getClientConfig({
    bundleName: 'catalog',
    publicPath: config.get('staticPath'),
    platform: 'touch-phone'
});
```

## get-server-config

Формирует конфиг для серверного бандла.

### Опции

Все опции не являются обязательными.

* `{String} bundleName` - Имя бандла. Дефолт - `''`
* `{String} bundlePath` - Путь к бандлу. Дефолт - `'./entries/<bundleName>/server.js'`
* `{String} publicPath` - Поле `publicPath`. Дефолт - `'/build/assets/'`
* `{String} serverBuildDir` - Путь куда собирать серверный код. Дефолт `'./build/server/'`
* `{String} platform` - Для какой платформы собирать. Дефолт - `'desktop'`

### Переменные окружения

* `NODE_ENV` - Окружение. Дефолт - `development`
* `HOT` - Включить `hot reload`

### Пример использования

```js
const getServerConfig = require('@realty-front/webpack-utils/get-server-config');

module.exports = getServerConfig({
    bundleName: 'catalog',
    platform: 'touch-phone'
});
```

## client-watcher

Запускает `webpack-dev-middleware` и `webpack-hot-middleware` для клиентских бандлов.

### Опции

Все опции не являются обязательными.

* `{String} hmrPath` - Путь для `webpack hmr`. Дефолт - `'/__webpack_hmr'`
* `{String} publicPath` - Поле `webpack.output.publicPath`. Дефолт - `'/build/assets'`
* `{String} configPath` - Путь до `webpack.config`. Дефолт - `'./.webpack.config.js'`

### Пример использования

```js
const clientWatcher = require('@realty-front/webpack-utils/client-watcher');

clientWatcher({
    hmrPath: '/cabinet/__webpack_hmr',
    configPath: './.webpack/configs/dashboard.js'
});
```

## server-watcher

Запускает `webpack` в `watch` режиме для серверных бандлов.

### Опции

Все опции не являются обязательными.

* `{String} configPath` - Путь до `webpack.config`. Дефолт - `'./.webpack.config.js'`

### Пример использования

```js
const serverWatcher = require('@realty-front/webpack-utils/server-watcher');

serverWatcher({
    configPath: './.webpack/configs/dashboard.js'
});
```

## webpack-utils-watch

Параеллельно запускает `<project>/.webpack/server-watcher.js` и `<project>/.webpack/client-watcher.js`.
Если одного из вотчеров нет, то пропускает его, если нет ни одного вонтчера, то 
завершается с ошибкой.

В `server-watcher.js` и `client-watcher.js` должны быть вызваны фукнции 
`server-watcher` и `client-watcher` из `webpack-utils`, как в примерах выше.

### Пример использования

```
tree <project>/.webpack

.webpack
├── client-watcher.js
└── server-watcher.js
```

Makefile
```
.PHONY: webpack-watch
webpack-watch:
	BUNDLE=$(bundle) HOT=1 NODE_ENV=$(YENV) $(REPO_BIN_DIR)webpack-utils-watch
```
