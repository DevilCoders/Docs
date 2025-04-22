[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/logger)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/logger) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/logger)](https://oko.yandex-team.ru/pkg/@yandex-market/logger)

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
