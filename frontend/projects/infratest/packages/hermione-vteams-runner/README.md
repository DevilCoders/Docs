# hermione-vteams-runner

Плагин позволяет запускать тесты только для определенного **vteam**.

## Установка

```bash
$ npm install @yandex-int/hermione-vteams-runner --registry=http://npm.yandex-team.ru
```

Подключить плагин в конфиге `hermione`

Минимальный конфиг:
```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-vteams-runner': {
            enabled: true,
        }
    },

    // ...
};
```

Теперь можно запускать hermione:
```bash
$ npx hermione --vteam=Velocity
```

Также плагин экспортирует метод для построения таблицы `{<absoluteFilePathToTest>: <vteamName>}`.
```js
    const vteamsRunner = require('@yandex-int/hermione-vteams-runner');

    const table = await vteamsRunner.api.buildLookupTable();
};
```
