# Yandex-logger stream for error-booster

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.qloud-logger-errors/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.qloud-logger-errors)<br>
![dist health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.qloud-logger-errors)
](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.qloud-logger-errors)

## Установка

```bash
npm install @yandex-int/messenger.qloud-logger-errors --save --registry=http://npm.yandex-team.ru
```

## Использование:

```js
const yandexLogger = require('yandex-logger');
const defaultStream = require('yandex-logger/streams/default');
const defaultMiddlewares = require('yandex-logger/middleware/preset-default');

const {
    stream,
    isQloud,
    yandexuidMiddleware,
} = require('@yandex-int/messenger.qloud-logger-errors');

const loggerConfig = {
    name: 'Project test',
    streams: [
        {
            level: 'info',
            stream: defaultStream(),
        },
        isQloud() && {
            level: 'warn',
            stream: stream({
                booster: config,
            }),
        },
    ].filter(Boolean),
    middleware: [
        yandexuidMiddleware,
        ...defaultMiddlewares(),
    ]
};

module.exports = yandexLogger({
    roject: 'test',
    env: 'testing',
    version: '1.2.3'
});
```

или

```ts
import * as yandexLogger from 'yandex-logger';
import defaultStream from 'yandex-logger/streams/default';
import defaultMiddlewares from 'yandex-logger/middleware/preset-default';

import {
    stream as errorBoosterStream,
    ErrorBoosterFields,
    isQloud,
    yandexuidMiddleware,
} from '@yandex-int/messenger.qloud-logger-errors';

const boosterConfig: ErrorBoosterFields = {
    roject: 'test',
    env: 'testing',
    version: '1.2.3'
};

const loggerConfig = {
    name: 'Project test',
    streams: [
        {
            level: 'info',
            stream: defaultStream(),
        },
        isQloud() && {
            level: 'warn',
            stream: errorBoosterStream({
                booster: boosterConfig,
            }),
        },
    ].filter(Boolean),
    middleware: [
        yandexuidMiddleware,
        ...defaultMiddlewares(),
    ]
};

export default yandexLogger.default(loggerConfig);
```
