# Clement

**DEPRECATED: clement устарел, используйте [kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html).**

node.js приложение для записи и воспроизведения HTTP запросов.

Форкнут от templar 12.3.0.

## Установка

```bash
npm install @yandex-int/clement --registry http://npm.yandex-team.ru
```

## Запуск

```bash
npx clement start
```

## Пример использования

Структура проекта:

```
.config/
    clement/
        cache/
        plugins/
            cache-key.js
        config.js
.yproject
package.json
```

В `.yproject` нужно указать путь до директории clement:

```json
{
  "paths": {
    "clement": "./.config/clement"
  }
}
```

Пример `.config/clement/config.js`:

```js
'use strict';

const path = require('path');

module.exports = {
    sources: {
        // Порт, на котором будет слушать clement и проксировать запросы на https://yandex.ru
        3333: {
            url: 'https://yandex.ru',

            // Конфигурационные секции, позволяющие переопределить параметры проксирования
            // и набор плагинов на основе сопоставления с запросом (функции-матчера).
            configs: [
                {
                    // Матчер по умолчанию сопоставляет `cfg.path` (массив строк или регулярных выражений) с `req.parsedURL.pathname`.
                    // matcher: (cfg, req) => true,

                    // Путь URL, для которого будет применен конфиг.
                    path: /.*/,

                    // Переходить по редиректам (или нет) при проксировании.
                    // Параметр передается в запрос за ответом бэкэнда, который мы делаем при помощи got (https://github.com/sindresorhus/got#followredirect).
                    followRedirect: true,

                    // Плагины выполняются перед плагинами самого clement.
                    plugins: [
                        require('./plugins/cache-key')
                    ],

                    // Где хранить дампы (по умолчанию – .config/clement/cache).
                    cachePath: path.resolve(__dirname, '..', 'dumps'),

                    // Переопределение параметров запроса:
                    // protocol, host, port, method, path, query, headers, body
                    source: {
                        headers: { 'x-foo': 42 },
                        query: { foo: 'bar' }
                    }
                }
            ]
        },
        // ...
    }
};
```

Пример плагина – `.config/clement/plugins/cache-key.js` (опционально):

```js
'use strict';

module.exports = {
    'cache-key': (ctx, next) => {
        if (!ctx.cache.key) {
            // В реальности нужно строить ключ на основе запроса.
            // По умолчанию ключ строится на основе method, path, query и sha256(body) запроса.
            // Не нужно хэшировать ключ – он и так будет хэширован.
            ctx.cache.key = 'foo';
        }

        next();
    }
};
```

Если поведение какого-либо маршрута нужно изменить полностью (например, поставить заглушку), то можно написать специальный контроллер.
Пример контроллера – `.config/clement/plugins/controllers/stub.js` (опционально):

```js
'use strict';

module.exports = {
    'controller': (ctx, next) => {
        const reqPath = ctx.req.parsedURL.path;

        // Лучше ставить контроллер на конкретный путь, здесь же для примера.
        if (!reqPath.startsWith('/api/v1/status')) {
            return next();
        }

        ctx.res.writeHead(200, {'content-type': 'application/json'});
        ctx.res.end('{"status": "ok"}');
    }
};
```

И добавить в конфигах:
```js
    ...
        configs: [
            {
                path: /^api\/v1/,
                plugins: [
                    require('./plugins/controllers/stub.js'),
                ]
            }
        ]
    ...
```

Теперь можно запустить clement в режиме записи ответов:

```bash
npx clement start --cache-mode=write
```

После того, как прокси будет поиспользован, а кэш наполнен, можно запустить clement в режиме чтения:

```bash
npx clement start --cache-mode=read
```

### Переопределение функции-матчера

Матчер может быть определен глобально, на уровне источника и на уровне конкретной конфигурационной секции (см. пример выше).

Пример переопределения матчера для express-like маршрутов на уровне источника:

```js
'use strict';

const pathToRegexp = require('path-to-regexp');
const {zipObject} = require('lodash');

const routeMatcher = (cfg, req) => {
    if (cfg.method && cfg.method !== '*' && cfg.method !== req.method) {
        return false;
    }

    let routeRe = cfg._routeRe;
    if (!routeRe) {
        cfg._routeKeys = [];
        cfg._routeRe = routeRe = pathToRegexp(cfg.route, cfg._routeKeys);
    }

    const parsedParams = routeRe.exec(req.parsedURL.pathname);
    if (!parsedParams) {
        return false;
    }

    // Не самый хороший вариант:
    // 1) Не покрывает все случаи `pathToRegexp`.
    // 2) Пишет в `cfg`, а не в `ctx` – можно исправить с помощью плагина на хуке `pre-data-fetch`.
    cfg.params = zipObject(cfg._routeKeys.map(k => k.name), parsedParams.slice(1));

    return true;
};

module.exports = {
    sources: {
        3333: {
            url: 'https://yandex.ru',
            matcher: routeMatcher,
            configs: [
                {
                    route: '/api/v1/entities/:id/sub/:subId'
                    plugins: [
                        // ...
                    ]
                },
                {
                    method: 'GET',
                    route: '/blog/:slug*',
                    plugins: [
                        // ...
                    ]
                }
            ]
        }
    }
};
```

### Инъекция middleware

Внутри clement поднимается connect с базовыми middleware для разбора запроса. При необходимости, можно дополнить middleware стэк, в том числе кастомными обработчиками ошибок. Если ошибка произошла при проксировании запроса на бэкенд - объект ошибки будет обогащен контекстом обработки запроса (аналогично контекста в плагинах).

```js
'use strict';

const {
    defaultMiddlewares
} = require('@yandex-int/clement')

module.exports = {
    middlewares: env => {
        return [
            (req, res, next) => {
                // ...
                next();
            },
            ...defaultMiddlewares(env)
        ];
    },
    sources: {
        // ...
    }
};
// ...
// или
// ...

const {
    middlewares: {
        busboy,
        bodyParser,
        cookieParser,
        compression,
        urlParser,
        bodyUnifier,
        routes,
        errorHandler
    }
} = require('@yandex-int/clement')

module.exports = {
    middlewares: env => {
        // чтобы connect понимал, что это обработчик ошибки - у функции должно быть ровно 4 аргумента
        const myErrorHandler = (err, req, res, next) => {
            if (err.ctx && err.ctx.requestMeta) {
                switch (err.ctx.requestMeta.errorCode) {
                    case 'ECONNREFUSED':
                    case 'ECONNRESET':
                    case 'ETIMEDOUT':
                    case 'ERR_SOCKET_BAD_PORT':
                        // ...
                }
            }

            next(err)
        };

        return [
            urlParser(),
            compression(),
            busboy(),
            bodyParser.raw({
                type: req => (!req.headers['content-type'] || req.headers['content-type'].includes('application/octet-stream'))
            }),
            bodyParser.urlencoded({extended: true}),
            bodyParser.json(),
            bodyParser.text(),
            cookieParser(),
            bodyUnifier(),
            routes(env),
            // вставляем наш хендлер
            myErrorHandler,
            errorHandler()
        ];
    },
    sources: {
        // ...
    }
};
```

## Устройство

Работа clement строится на идее цепочек плагинов и хуков – точек вызова плагинов.

Точка входа – запуск цепочки плагинов, висящих на хуке `controller` (`middlewares/routes`). Контроллеры также являются плагинами, но запускаются самим clement.

Контроллер по умолчанию (`plugins/controllers/proxy`) запускает цепочки плагинов, висящие на хуках:

- `pre-data-fetch`
- `data-fetch`
- `post-data-fetch`

### Плагины `pre-data-fetch`:

- `source-request` – наполняет `ctx.sourceReq` из оригинального запроса. Запрос в конкретный источник будет произведен на основе данных из `ctx.sourceReq`.

### Плагины `data-fetch`:

- `file-cache/pluginDataFetchFileCache` – читает дампы. Не работает в режиме записи дампов (`--cache-mode=write`). Предварительно запускает хуки для формирования данных о дампе:

  - `cache-key`, плагины:
    - `dump-id` – добавляет обязательный параметр в `ctx` (тот, что был указан в `--required-param`). Используется для привязки дампа к конкретному тесту.
    - `cache-key` – формирует ключ дампа на основе данных запроса.
    - `cache-sequence` – формирует возрастающий счетчик для ключа дампа. Используется для записи различных дампов идентичных запросов (необходим запуск с `--cache-sequence` или обязательный параметр должен содержать суффикс `_seq`).

  - `cache-filepath`, плагины:
    - `cache-filepath` – формирует путь, где складываются дампы.

  - `cache-filename`, плагины:
    - `cache-filename` – формирует имя файла дампа.

  - `cache-patch`, плагины:
    - `cache-patch` - определяет логику получения и применения патчей. Про патчи можно подробнее почитать [в соответствующем разделе](#патчи-на-дампы).

- `proxy` – производит запрос в источник и наполняет `ctx.sourceRes` из ответа (без каких-либо модификаций).
Плагин складывает дополнительную мета-информацию о запросе (метод запроса, время выполнения, код ответа, URL) в контекст (`ctx.requestMeta`).

### Плагины `post-data-fetch`:

- `file-cache/pluginPostDataFetchFileCache` – пишет дампы. Работает только в режиме записи дампов (`--cache-mode=write|create`). Предварительно запускает хуки для формирования данных о дампе:

  - `cache-key`
  - `cache-filepath`
  - `cache-filename`
  - `cache-meta`, плагины:
    - `cache-meta` – добавляет мета информацию о запросе в дамп.
  - `cache-patch-drop`, плагины:
    - `cache-patch-drop` - определяет логику удаления патчей.

- `source-response` – модифицирует `ctx.sourceRes` перед отдачей ответа клиенту (удаляет специфичные заголовки и т.д.).

### Очередность плагинов по умолчанию:

```js
// pre-data-fetch
'source-request',

// data-fetch & post-data-fetch
'dump-id',
'cache-key',
'cache-sequence',
'cache-filepath',
'cache-filename',
'cache-meta',
'file-cache/migration',
'file-cache',
'cache-patch',
'cache-patch-drop',

// data-fetch, строго после кеша
'proxy',

// post-data-fetch
'source-response',

'controllers/proxy'
```

## Миграция дампов clement с версии 2- на версию 3+

Для миграции дампов следует использовать опцию `--from2to3` (или переменную окружения `FROM_2_TO_3` со значением `true`) в режиме чтения дампов. Требование миграции при воспроизведении тестов происходит из потребности учитывать проектные кастомизации и отсутствия всей необходимой для миграции дампов информации в самих дампах. Рекомендуемым способом при этом является использование gui-режима, в котором появляется возможность перезапуска только упавших тестов, что полезно при миграции больших наборов сьютов, при которых возможны единичные падения.

## Просмотр информации о дампах

Для просмотра информации о дампах можно использовать команду `show` с обязательной опцией `-p` (`--path`), указывающей на директорию, информацию о дампах из которой нужно получить, или на конкретный дамп. Данная команда очень похожа на одноименную команду [темплара](../templar). По умолчанию будет выведен незахешированный ключ дампа:

```bash
> npx clement show -p test-data/
path/to/dump/dump-0.json.gz body=90f159d14c0dd801668fef4685def2ce10ea38876b3f1eba8cc24eccc3d62d90&method=post&path=/json

path/to/dump/dump-1.json.gz      login=false&lr=213&text=clement&tld=ru
```

Опция `-u` (`--url`) выводит урл запроса:

```bash
> npx clement show -p test-data/ -u
path/to/dump/dump-0.json.gz     /json

path/to/dump/dump-1.json.gz     /search/pad/?text=clement&lr=213
```

Опция `-v` (`--verbose`) выводит мета-информацию о запросе (ключ, урл, метод, детали ответа).

Опция `-m` (`--match`) позволяет дополнительно отфильтровать дампы по ключу или урлу по указанной подстроке и выводит результат с учетом рассмотренных выше опций:

```bash
> npx clement show -p test-data/ -u -m 'text=clement'
path/to/dump/dump-1.json.gz      /search/pad/?text=clement&lr=213
```

## Патчи на дампы

Существует возможность создания патчей для дампов json-ответов, которые при воспроизведении (режим `play`) будут модифицировать исходное тело ответа, содержащееся в дампе. При переснятии (режим `write`) такие патчи будут удаляться автоматически. Патч можно создать, положив его в одну директорию с соответствующим дампом и присвоив ему такое же название, за исключением расширения - `.patch.js` вместо `.json.gz`.

Патч представляет собой стандартный commonjs-модуль, экспортирующий либо функцию для модификации ответа, либо объект, который будет с помощью lodash-функции `merge` объединен с исходным ответом. Функция принимает единственный аргумент - исходный json-ответ и должна возвращать результирующий json-ответ.

Пример функции-патча:

```js
// данный патч удаляет поле "extraField" из ответа
module.exports = function(data) {
    delete data.extraField;
    return data;
}
```

Пример объекта-патча:

```js
// данный патч добавляет или переопределяет поле "deep.extraField"
module.exports = {
    deep: {
        extraField: 10,
    }
}
```

Кроме того, существует возможность переопределения механизма кеширования на проекте за счет переопределения плагинов `cache-patch` и `cache-patch-drop`, которые вызываются при воспроизведении и переснятии дампов соответственно.

### Создание патчей

Патчи можно создавать как вручную, так и воспользоваться командой `patch`. Эта команда наподобие команды [`show`](#просмотр-информации-о-дампах) позволяет с помощью сходных опций `-p` и `-m` сматчить необходимый дамп, для которого нужен патч и создает дефолтную реализацию патча:

```bash
# команда show выводит сматченный дамп
> npx clement show -p test-data/ -u -m 'text=clement'
path/to/dump/dump-1.json.gz      /search/pad/?text=clement&lr=213

# команда patch создает патч для него
> npx clement patch -p test-data/ -u -m 'text=clement'
Патч "/Users/user/project/test-data/path/to/dump/dump-1.patch.js" создан.
```

Опции `-p` и `-m` должны указывать на единственный дамп для создания патча.

Создаваемый патч по умолчанию выглядит так:

```js
'use strict';
// Патч должен возвращать конечные данные ответа (необязательно исходные)
module.exports = function(data) {
    return data;
};
```

## Требования

- node.js >= 8.4
