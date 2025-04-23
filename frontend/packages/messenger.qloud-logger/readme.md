# Qloud-logger

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.qloud-logger/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.qloud-logger)<br>
![dist health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.qloud-logger)
](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.qloud-logger)

## Установка

```bash
npm install @yandex-int/messenger.qloud-logger --save --registry=http://npm.yandex-team.ru
```

## Использование

```ts
import { createLogger, createLogMiddleware, createErrorMiddleware } from '@yandex-int/messenger.qloud-logger';

const logger = createLogger({
    name: 'my-super-service'
});

app.use(createLogMiddleware(logger));

app.use(createErrorMiddleware());
```
