## Tune logger

Обвязка для [log4js](https://www.npmjs.com/package/log4js) для простой поставки логов через unified agent.

### Состав

- **logger.js** дополняет контекст логгера полями из req
- **http-appender.js** аппендер для записи в http вход, который использует unifier agent
- **layouts.js** два лейаута, приспособленных для получения ошибок в виде объектов как у [rum.logError](https://a.yandex-team.ru/arc_vcs/velocity/error-booster/error-counter/#отправка-кастомной-ошибки)



### Быстрай старт ###

0. Установите модуль и логгер log4js (если вы не собираетесь использовать http-appender с другим логгером).
```
npm i --save @yandex-int/tune-logger log4js@3.0.5
```

1. Логгер должен быть сконфигурирован при старте вашего приложения. Функция `configure` принимает единственный параметр - [конфиг log4js](https://log4js-node.github.io/log4js-node/api.html), и ничего не возвращает.
```js
const {
    configure,
    getDefault,
    getLogger

} = require('@yandex-int/tune-logger');

configure({
    "appenders": {
        /* для отправки через агент */
        "unified": {
            "type": "@yandex-int/tune-logger/http-appender.js",
            /* должен быть указан порт unified agent'а */
            "port": 22132,
            /* путь в ручке unifiedagent после слеша. например localhost:22132/write */
            "path": "write",
            "layout": {
                /* встроено в tune-logger */
                "type": "json-layout",
                "tokens": {
                    "env": "<окружение (developent, testing, production)>",
                    "project": "<ваш проект в error-booster'e>",
                    "version": "<версия вашего приложения>"
                }
            }
        },
        /* для человекочитаемого лога в консоль */
        "console": {
            "type": "stdout",
            "layout": {
                /* встроено в tune-logger */
                "type": "plain-pattern",
                "pattern": "%d{yyyy.MM.dd hh:mm:ss.SSS} [%z] %[%p] [%X{reqid}] %m %]"
            }
        }
    },
    "categories": {
        "default": {
            "appenders": ["unified", "console"],
            "level": "info"
        }
    }
});
```

2. После конфигурации можно получать дефолтный логгер с не полным набором параметров (без `reqid, yandexuid, useragent, ip, page, url, method`), либо получить полный логгер, передав req:

```js
let defaultLogger = getDefault();
defaultLogger.info({
    message: 'hello, logger'
});
...
app.use(function (req, res, next) {
    req.request_id = '.....'; // Ваш любимый способ генерации id запроса

    /* default - название категории из конфига */
    req.logger = getLogger(req, 'default');
    req.logger.info({
        message: 'hello from request'
    });
    next();
});
```

Как и в rum.logError, вторым параметром можно передать объект ошибки
```js
app.use(function (error, req, res, next) {
    req.logger.error({
        message: 'oh no, unexpected error!'
    }, error);
});
```

3. Для более полного логирования добавляйте в контекст логгера свойства
 - **yandexuid**
 - **region** id региона из геобазы
 - **platform** платформа (desktop/touch)


4. Настройте http input в unified agent'е.
Примерно так, подробности в [документации агента](https://docs.yandex-team.ru/unified_agent/configuration/inputs#http_input)

```yml
routes:
  - input:
      plugin: http
      config:
        # должен быть тот же порт,
        # что и в конфиге логгера
        port: 22132
```

### FAQ


Q: Почему такая старая версия log4js?

A: В новой версии выпилили `addContext`, который нужен для дополнения сообщений информацией


Q: Как дебажить отправку в unified agent?

A: Зaпустить приложение с env переменной `DEBUG=tune-logger` или даже `DEBUG="tune-logger,log4js:*"`
