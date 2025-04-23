#### Запуск тестов

```sh
npm i
npm test
```

#### Просмотр результатов покрытия

```sh
open coverage/lcov-report/index.html
```

#### Выпуск новой версии

1. В зависимости от масштаба изменений делаем `npm version minor` или `npm version patch` согласно semver.
(minor: X.Y.Z -> X.Y+1.Z, patch: X.Y.Z -> X.Y.Z+1)

    npm version minor

2. Пушим изменения в `package-lock.json`, `package.json` и тег новой версии

    git push --tags ... # здесь надо уточнить

3. Чистим локальную копию от мусора и ignored-файлов и делаем publish

    npm publish --registry https://npm.yandex-team.ru
