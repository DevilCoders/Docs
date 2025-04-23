![Yandex Logger Logo](https://yastatic.net/q/logoaas/v1/Yandex%20Logger.svg?size=100)

Расширяемый логгер для node.js приложений, умеющий из коробки логировать в Qloud, Deploy, Sentry и Error Booster.

[![oko yandex-logger](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/yandex-logger)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/yandex-logger)

* [Особенности](#Особенности)
* [Подключение к проекту](#Подключение-к-проекту)
* [Использование](#Использование)
    * [Создание логгера](#Создание-логгера)
    * [Уровни логирования](#Уровни-логирования)
    * [Интерфейс логирования](#Интерфейс-логирования)
    * [Дополнительные данные в логах](#Дополнительные-данные-в-логах)
    * [Предопределенные свойства req, err и другие](#Предопределенные-свойства-req-err-и-другие)
    * [Создание дочернего логгера](#Создание-дочернего-логгера)
    * [Создание логгера per-request](#Создание-логгера-per-request)
    * [Логирование запросов в express](#Логирование-запросов-в-express)
    * [Проектный логгер в виде пакета](#Проектный-логгер-в-виде-пакета)
* [Конфиг](#Конфиг)
    * [Настройки по умолчанию](#Настройки-по-умолчанию)
* [Формат логов](#Формат-логов)
    * [Как написать свой стрим](#Как-написать-свой-стрим)
    * [Настройки стримов](#Настройки-стримов)
    * [Готовые стримы](#Готовые-стримы)
        * [raw json](docs/stream-json.md)
        * [Форматированный текст](docs/stream-line.md)
        * [Qloud](docs/stream-qloud.md)
        * [Deploy](docs/stream-deploy.md)
        * [Sentry](docs/stream-sentry.md)
        * [Error Booster](docs/stream-error-booster.md)
* [Обработка логов](#Обработка-логов)
    * [Как написать middleware](#Как-написать-middleware)
    * [Стандартные мидлвары](#Стандартные-мидлвары)
        * [err](middleware/err.js)
        * [req](middleware/req.js)
        * [request-id](middleware/request-id.js)
        * [blackbox](middleware/blackbox.js)
        * [secure-cookie](middleware/secure-cookie.js)
        * [secure-field](middleware/secure-field.js)
        * [secure-passport-cookie](middleware/secure-passport-cookie.js)
        * [secure-tvm-headers](middleware/secure-tvm-headers.js)
        * [bunyan](middleware/bunyan.js)
    * [Пресеты мидлвар](#Пресеты-мидлвар)
        * [preset-default](middleware/preset-default.js)
        * [preset-security](middleware/preset-security.js)
* [Express-middleware](#express-middleware)
* [Examples](#examples)
* [Benchmarks](#benchmarks)
* [Тесты](#тесты)

------------

## Особенности

* Имеет гибкий интерфейс логирования, подходящий под любые проекты
* Расширяемость во всем: форматы логирования, способы обработки данных
* Не имеет ограничений на формат и количество логируемых данных
* Умеет из коробки логировать в формате Qloud, Deploy, Sentry и Error Booster
* Умеет шаблоны для форматирования логов в stdout и stderr
* Поставляется с набором мидлвар, необходимых для инфраструктуры Яндекса
* Обеспечивает безопасность логов: обфусцирует чувствительные данные (например, паспортные cookie)
* Полное покрытие тестами
* Поддержка Node.js 4+


## Подключение к проекту

```bash
npm install @yandex-int/yandex-logger --save
```

## Использование

### Создание логгера

Логгер можно использовать без конфига. В таком случае логгер автоматически выберет в каком формате логировать: qloud json или тестовые строки.
```js
const logger = require('yandex-logger')();

logger.info('Hello world!');
```

Можно настроить имя логгера и формат логов:
```js
const logger = require('yandex-logger')({
    name: 'my-app',
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/qloud')()
        }
    ]
});

logger.info('Hello world!');
```

### Уровни логирования

Методы перечислены в порядке увеличения веса:

```js
logger.trace('Привет');
logger.debug('Привет');
logger.info('Привет');
logger.warn('Привет');
logger.error('Привет');
logger.fatal('Привет');
```

### Интерфейс логирования

Строки форматируются через модуль [pff](https://www.npmjs.com/package/pff), поэтому поддерживаются только `%s` и `%d`.

Примеры:

```js
// Можно логировать просто строки
logger.info('Просто строка');
logger.info('Просто строка с параметрами %s %d', 'параметр', 123);

// Дополнительные данные можно передавать первым аргументом
const data = { foo: 'дополнительные данные' };
logger.info(data); // будет пустое сообщение, но зато с данными ;)
logger.info(data, 'Просто строка');
logger.info(data, 'Просто строка с параметрами %s %d', 'параметр', 123);

// Exception можно передать первым параметром, либо внутри данных в свойсте `err`
const err = new Error('test');
logger.info(err); // сообщение будет взято из err.message
logger.info({ err, ...data }); // сообщение будет взято из err.message
logger.info(err, 'Переопределяем сообщение');
logger.info(err, 'Переопределяем сообщение с параметрами %s %d', 'параметр', 123);
```

### Дополнительные данные в логах

Логгер позволяет добавлять абсолютно любые данные в лог. Для этого нужно передавать объект с данными первым аргументом:

```js
logger.error({
    req,
    err,
    user: {
        id: 123,
        name: 'Вася'
    },
    status: 500
}, 'Что-то случилось');
```

### Предопределенные свойства req, err и другие

В логгере есть ряд соглашений про названия свойств в объекте с данными.
Свойства являются необязательными, но на них рассчитывают стандартные мидлвары и стримы.

* `{String} name` – название приложения, модуля или другой структурной единицы
* `{Request} req` – информация о текущем http запросе, можно передавать полновесный req
* `{Error} err` – инстанс ошибки, из которой будет браться сообщение и стектрейс
* `{String} group` – уникальный ключ для группировки записей в Sentry
* `{Object} sentry` – любые данные, которые должны попадать только в стрим Sentry

### Создание дочернего логгера

К инстансу логгера можно забиндить данные, чтобы не передавать их каждый раз при логировании.

Чтобы дополнить данные в инстансе, вызываем метод `logger.extendFields()`:
```js
const logger = require('yandex-logger')({ name: 'app-1' });

logger.info('Привет'); // name=app-1, Привет

logger.extendFields({ name: 'app-2', release: '1.2.3' });
logger.info('Привет'); // name=app-2, release=1.2.3, Привет
```

Часто возникает необходимость создать новый логгер, расширив данные для существующего логгера через `logger.child()`:
```js
const logger = require('yandex-logger')({
    name: 'app',
    fields: {
        version: '2.5.0'
    }
});

const dbLogger = logger.child({ name: 'db' });
const apiLogger = logger.child({ name: 'api', requestId: 'req-123' });

logger.info('Привет'); // name=app, version=2.5.0, Привет
dbLogger.info('Привет'); // name=db, version=2.5.0,Привет
apiLogger.info('Привет'); // name=api, version=2.5.0, requestId=req-123, Привет
```

### Создание логгера per-request

Иногда бывает удобно часть полей забиндить для всех логов в рамках запроса:
```js
const logger = require('yandex-logger')(config);

app.use((req, res, next) => {
    // Закидываем req во все логи, оттуда сможем взять:
    // - полный url запроса
    // - заголовки
    // - request id
    // - пользователя
    // и все остальное, что сами захотим залогировать через собственные мидлвары
    req.logger = logger.child({ req });

    next();
});
```

Далее логгер можно использовать так:
```js
app.use((req, res, next) => {
    // Передаем инстанс логгера в api, чтобы логи содержали информацию о запросе
    req.api = new Api({ logger: req.logger });

    // Просто логируем что-нибудь
    req.logger.info('Привет');

    next();
});
```

### Логирование запросов в express

Часто возникает потребность залогировать HTTP запрос и его тайминг.

Через yandex-logger и express это делается примерно так:
```js
const logger = require('yandex-logger')({ name: 'http-request' });

app.use((req, res, next) => {
    req.time = Date.now();

    function log() {
        const time = ((Date.now() - req.time) / 1000).toFixed(3);

        // Будет выводить в лог для каждого запроса:
        // GET  /some-url  200  0.256s
        logger.info('%s %s %d %ss', req.method, req.url, res.statusCode, time);
    }

    res.on('finish', log);
    res.on('close', log);

    next();
});
```

По возможности нужно разместить мидлвару самой первой, чтобы отсчитывать время с самого начала обработки запроса. Можно добавить цветной вывод через модуль chalk.

### Проектный логгер в виде пакета

Если у вас в проекте есть необходимость использовать логгер в разных пакетах, но с одинаковыми настройками, то удобно создать модуль с проектным логгером:
```js
// my-logger/index.js

module.exports = require('yandex-logger')({
    name: 'my-app',
    streams: [
        // Настройки стримов под проект
    ],
    middleware: [
        // Проектные мидлвары
    ]
});
```

Использовать можно так:
```js
const logger = require('my-logger');
logger.info('Привет');

const apiLogger = logger.child({ name: 'api' });
apiLogger.info('Привет от api');
```

Например, в Афише есть пакет [afisha-logger](https://github.yandex-team.ru/afisha-frontend/afisha-logger), который используется в десятке других модулей.

## Конфиг

Доступные опции:

```js
const config = {
    // Название логгера, по умолчанию `yandex-logger`.
    // Можно использовать для разграничения логов по частям приложения.
    name: 'my-app',

    // Массив стримов, в которые нужно оправлять логи.
    // По умолчанию содержит один стрим `yandex-logger/streams/default` с уровнем `info`.
    streams: [
        {
            level: 'info',
            stream: require('yandex-logger/streams/qloud')()
        },
        {
            level: 'info',
            stream: require('yandex-logger/streams/sentry')()
        },
    ],

    // Набор функций для предобработки логов.
    // По умолчанию содержит только `yandex-logger/middleware/preset-default`.
    middleware: [
        require('yandex-logger/middleware/preset-default')(),
        require('./custom-middleware')()
    ],

    // Любые дополнительные данные, которые нужно добавить в каждую запись в логах.
    fields: {
        release: '1.2.3',
        environment: process.env.NODE_ENV
    }
};
```

### Настройки по умолчанию

Стандартный конфиг:
```js
const config = {
    name: 'yandex-logger',
    streams: [
        {
            level: 'info',
            stream: require('./streams/default')()
        }
    ],
    middleware: [
        require('./middleware/preset-default')()
    ],
    fields: {}
};
```

Логгер со стандартным конфигом будет:

* Писать сообщения с уровнем info и выше
* Писать сообщения в текстовом формате во время разработки: `[date] [level]: [message]`
* Писать сообщения в формате Qloud при наличии переменной окружения `QLOUD_LOGGER_STDERR_PARSER`
* От большого `req` оставлять в логах только необходимое: полный url с хостом, метод, заголовки, тело запроса
* Превращать `err` в сериализуемый объект, сохраняя все кастомные свойства
* Вытаскивать из `req` и добавлять в лог request id
* Вытаскивать из `req` и добавлять в лог данные про пользоватля: uid, login, email
* Обфусцировать в логах паспортные cookie: `Session_id, Secure_session_id, sessionid2`
* Обфусцировать в логах TVM токены в заголовках: `ticket, x-ya-user-ticket, x-ya-service-ticket`
* Обфусцировать в логах значения заголовока `Authorization`

Любую из фукций можно дополнить или отключить через конфиг.

## Формат логов

Стримы – это способ записать лог в определенном формате. Стримов может быть много в одном логгере.

### Как написать свой стрим

Любой стрим – это Writable объект. В простейшем случае стрим выглядит так:
```js
// console-stream.js
module.exports = () => {
    // В эту функцию можно принимать конфиг стрима

    // Возвращаем Writable объект, это и есть стрим
    return {
        /**
         * @param {Object} record – Лог запись
         */
        write(record) {
            /*
             * Пример простейшей записи:
             * {
             *     name: 'my-app',
             *     pid: 123,
             *     date: new Date(),
             *     hostname: 'localhost',
             *     level: 50,
             *     levelName: 'ERROR',
             *     msg: 'Привет, мир!',
             *     msgFormat: 'Привет, %s!',
             *     msgArgs: ['мир']
             * }
             */
            console.log(record);
        }
    };
};
```

Использовать этот стрим можно так:
```js
const logger = requrie('yandex-logger')({
    streams: [
        {
            level: 'info',
            stream: require('./my-stream')()
        }
    ]
});

logger.info('Привет'); // Выведет в консоль объект со свойством `msg: 'Привет'`
```

### Настройки стримов

Настройки всегда содержат два свойства

1. `{String} level` – минимальный уровень лога, который будет попадать в стрим
2. `{Writable} stream` – любой объект с функцией `write(record)`

Уровни и их вес:
* `trace = 10`
* `debug = 20`
* `info = 30`
* `warn = 40`
* `error = 50`
* `fatal = 60`

### Готовые стримы

* [raw json](docs/stream-json.md)
* [Форматированный текст](docs/stream-line.md)
* [Qloud](docs/stream-qloud.md)
* [Deploy](docs/stream-deploy.md)
* [Sentry](docs/stream-sentry.md)
* [Error Booster](docs/stream-error-booster.md)

## Обработка логов

Перед тем как отправить лог во все стримы, лог проходит предобработку через мидлвары. Этот механизм позволяет менять и дополнять поведение логгера под потребности проекта.

### Как написать middleware

Мидлвара – это просто функция, мутирующая объект лога. Пример простешей мидлвары:
```js
const logger = requrie('yandex-logger')({
    middleware: [
        // Это синхронная мидлвара
        record => {
            // Можно добавить новое поле
            record.newField = 'data';

            // Можно изменить существующие
            record.url = record.hostname + record.url;

            // Можно удалять существующие, чтобы они не попали в лог
            delete record.hostname;
        },

        // Мидлвары могут быть асинхронными
        (record, done) => {
            // например, можно отложить запись логов
            setTimeout(done, 1000);
        }
    ]
});
```

Объект `record` создается для каждой записи лога, поэтому его можно безопасно мутировать.

Состав данных в `record` определяется следующим образом:

1. Берутся стандартные поля (pid, name, date и т.д.)
2. Добавляются поля из конфига (свойство `fields`)
3. Добавляются поля, переданные в вызов `logger.child()` и `logger.extendFields()`
4. Добавляются поля, которые переданы в вызов логгера (`log.info(fields)`)
5. Запускаются все мидлвары, которые могут изменить состав полей
6. `record` отправляется в стримы

### Стандартные мидлвары

* [err](middleware/err.js) – Превращает исключения в сериализуемые объекты. Сохраняет кастомные поля в ошибках.
* [req](middleware/req.js) – Оставляет от большого `req` минимальный объем данных: метод, полный url с хостом, заголовки, тело запроса, yandexuid.
* [request-id](middleware/request-id.js) – Вытаскивает из `req` и добавляет в лог request id.
* [blackbox](middleware/blackbox.js) – Вытаскивает из `req` и добавляет в лог данные про пользователя: uid, login, email.
* [secure-cookie](middleware/secure-cookie.js) – Обсусфирцирует cookie в переданных полях.
* [secure-field](middleware/secure-field.js) – Обсусфирцирует любые значения в переданных полях.
* [secure-passport-cookie](middleware/secure-passport-cookie.js) – Обфусцирует паспортные cookie.
* [secure-tvm-headers](middleware/secure-tvm-headers.js) – Обсусфирцирует TVM заголовки.
* [bunyan](middleware/bunyan.js) – Добавляет совместимость с bunyan pipes.

### Пресеты мидлвар

Пресет - это просто набор мидлвар. Например:
```js
// my-preset.js
module.exports = () => {
    // Можно добавить конфиг для пресета

    return [
        // Набор мидлвар в пресете
        require('./middleware-1')(),
        require('./middleware-2')()
    ];
};
```

Далее логгер самостоятельно раскроет массивы любой вложенности.

Готовые пресеты:
* [preset-default](middleware/preset-default.js) – Все мидлвары из конфига по умолчанию.
* [preset-security](middleware/preset-security.js) – Обсускация паспортных cookie и TVM токенов.

## Express-middleware

В состав логгера включена express middleware для логирования запросов.

```js
const Express = require('express');
const createLogger = require('@yandex-int/yandex-logger');
const createRequestMiddleware = require('@yandex-int/yandex-logger/express-middleware/request');

const logger = createLogger(config);
const app = new Express();

app.use(createRequestMiddleware(logger));
```

Функция `createRequestMiddleware(logger: YandexLogger, messageCreator?: MessageCreator)` добавляет в request объект logger, который в дальнейшем можно использовать для отправки логов `req.logger = logger.child({ req })`.

По умолчанию, в поле message выводится `GET  /some-url  200  256ms`.
Выводимое сообщение можно изменить, передав вторым аргументом в createRequestMiddleware функцию messageCreator.
```js
messageCreator(
    {
        req,  // объект request, логирование выполняется через req.logger.info(...)
        res,  // объект response, res.responseTime - время выполнения запроса в ms
        err   // объект ошибки, если есть.
    },
    isClosed // true если сработало событие 'close', false если событие 'finish
)
```

## Examples

Все примеры можно посмотреть в директории `examples/`.

* [Уровни логирования](examples/log-levels.js)
* [Интерфейс логирования](examples/log-api.js)
* [Работа с дополнительными данными](examples/fields.js)
* [Полный конфиг](examples/config-all.js)
* [Конфиг по умолчанию](examples/config-zero.js)
* [Подключение стрима raw json](examples/stream-json.js)
* [Подключение стрима line](examples/stream-line.js)
* [Подключение стрима qloud](examples/stream-qloud.js)
* [Подключение стрима sentry](examples/stream-sentry.js)
* [Подключение стрима error booster](examples/stream-error-booster.js)

## Benchmarks

Запуск бенчмарков:

```bash
cd benchmark
npm install
node index.js
node comparison-qloud.js
node comparison-sentry.js
node comparison-std.js
```

Результаты ниже были получены на `MacBook Pro Retina 13" mid 2015`, Node.js 8.9.0

Результаты бенчмарка `index.js`:
```
[json]   Simple message x 143,829 ops/sec ±1.44% (84 runs sampled)
[json]   Message and data x 115,668 ops/sec ±1.91% (85 runs sampled)
[json]   Error x 103,985 ops/sec ±1.58% (89 runs sampled)
[std]    Simple message x 206,455 ops/sec ±2.67% (87 runs sampled)
[std]    Message and data x 183,561 ops/sec ±2.88% (89 runs sampled)
[std]    Error x 185,253 ops/sec ±0.78% (93 runs sampled)
[qloud]  Simple message x 136,349 ops/sec ±1.21% (91 runs sampled)
[qloud]  Message and data x 117,074 ops/sec ±1.12% (91 runs sampled)
[qloud]  Error x 88,285 ops/sec ±1.38% (90 runs sampled)
[sentry] Simple message x 5,108 ops/sec ±8.75% (69 runs sampled)
[sentry] Message and data x 3,933 ops/sec ±16.15% (57 runs sampled)
[sentry] Error x 2,623 ops/sec ±12.98% (59 runs sampled)
```

Результаты бенчмарка `comparison-std.js`:
```
[yandex-logger] Simple message x 675,271 ops/sec ±1.89% (86 runs sampled)
[bunyan]        Simple message x 502,108 ops/sec ±6.39% (80 runs sampled)
[pino]          Simple message x 300,368 ops/sec ±2.19% (92 runs sampled)
[kroniko]       Simple message x 945,709 ops/sec ±1.98% (82 runs sampled)
[yandex-logger] Message and data x 278,429 ops/sec ±4.31% (91 runs sampled)
[bunyan]        Message and data x 262,385 ops/sec ±3.50% (84 runs sampled)
[pino]          Message and data x 113,421 ops/sec ±1.44% (89 runs sampled)
[kroniko]       Message and data x 184,912 ops/sec ±1.23% (89 runs sampled)
[yandex-logger] Error x 324,906 ops/sec ±2.16% (91 runs sampled)
[bunyan]        Error x 284,407 ops/sec ±1.06% (90 runs sampled)
[pino]          Error x 107,738 ops/sec ±1.53% (91 runs sampled)
[kroniko]       Error x 948,400 ops/sec ±2.31% (90 runs sampled)
```

## Тесты

Запуск тестов:

```bash
npm install
npm test
```
