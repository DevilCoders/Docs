logger
======

Использование:
```js
const logger = require('@yandex-market/logger');

logger.info('Hello, world!');

if (logger.isEnabled('debug')) {
    somethingExpensive();
}
```

Доступные уровни:
```js
logger.trace(...args);
logger.debug(...args);
logger.info(...args);
logger.warn(...args);
logger.error(...args);
```

Для инициализации логгера используется функция `logger.setup(impl, maxLevel)`.
