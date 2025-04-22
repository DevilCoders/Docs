# @yandex-int/messenger.errors-light

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.errors-light/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.errors-light)<br>
![dist health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.errors-light)
](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.errors-light)

Пакет для очень легкого логирования ошибок в error booster.

## Install:

```
npm i @yandex-int/messenger.errors-light --registry=http://npm.yandex-team.ru
```

## Usage:

```
import { updateSettings, logError } from '@yandex-int/messenger.errors-light';

updateSettings({
    project: 'error-booster-project',
    version: process.env.VERSION,
    env: process.env.NODE_ENV,
});

getData()
    .catch((error) => {
        logError(error, { source: 'backend', additional: { foo: 'bar' }});
    });
```
