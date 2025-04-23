# tap-tanker-helpers 🌍

Пакет интернационализации турбо-приложений

## Установка
Для установки пакета следует выполнить в корне репозитория:
```bash
npx lerna add @yandex-int/tap-tanker-helpers --scope=<package-name>
```
где `<package-name>` - название пакета, куда нужно установить `tap-tanker-helpers`.

В проекте, в котором будет использован `tap-tanker-helpers`, установите утилиту `tanker-kit`

```bash
npm i tanker-kit --save-dev --registry http://npm.yandex-team.ru
```

Чтобы запуск установленного локально `tanker-kit` был доступен по короткому имени tanker, нужно установить пакет `tanker-cli`. Пакет `tanker-cli` - это хелпер, аналогичный `grunt-cli`, `bem-cli` и другим `cli`.

```bash
sudo npm i tanker-cli -g --registry http://npm.yandex-team.ru
```

## Дополнительная документация
- [Readme tanker-kit](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/tanker-kit/README.md)

- [Wiki tanker-kit](https://wiki.yandex-team.ru/search-interfaces/tanker/tanker-kit/)

- [Wiki танкера](https://wiki.yandex-team.ru/NikitaBrovikov/tanker/translator/)

- [Документация танкера](https://doc.yandex-team.ru/~infrastructure/~tanker/)

## Использование

Танкер использует oauth-токен для авторизации к своему API. Для генерации персонального токена перейдите по ссылке https://nda.ya.ru/3SjQY7. Затем экспортируйте ключ в `$HOME/.profile` (или `.bash_profile`, если не сработало), добавив
`export TANKER_API_TOKEN="OAuth токен для Танкера"`.

В корне проекта создать папку `.tanker` и создать в ней файл `config.js`. Про дополнительную конфигурацию танкера можно прочитать в [документации](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/tanker-kit/README.md).

Пакет экспортирует функции `getI18nKeys` и `extractI18NKeysFromSourceFile`.

_Пример использования `getI18nKeys`_
```ts
const tanker = require('tanker-kit');
const { getI18nKeys } = require('@yandex-int/tap-tanker-helpers');

module.exports = function dispatch(arg) {
    const config = arg.info.config;

    return tanker
        .find(config)
        .then(paths => tanker.parse(paths, config))
        .then(parsedKeys => getI18nKeys(parsedKeys, arg.data));
};
```

Функция используется для генерации контента для файлов переводов.

_Пример использования `extractI18NKeysFromSourceFile`_
```ts
module.exports = function({ data: content, path: filePath }) {
    const keys = extractI18NKeysFromSourceCode(content, path.basename(filePath), ['i18n']);
    const keyset = path.dirname(filePath);

    return keys
        .map(key => {
            const { name, range, params, context, value } = key;
            const keyAdapter = {
                type: 'bem',
                hash: getHash(key, filePath),
                path: filePath,
                range,
                upload: null,
                single: (isString(keyset) && isString(name)) || null,
                keyset,
                key: isString(name) ? name : null,
                value: value,
                comment: '',
                context: context || '',
                plural: null,
                params: Array.isArray(params)
                    ? params.reduce(function(acc, param) {
                          return Object.assign({}, acc, param);
                      }, {})
                    : false,
            };

            return { key: keyAdapter };
        })
        .map(({ key }) => {
            if (key.context) {
                key.params = { context: key.context };
            }

            return key;
        });
};
```

Функция используется для получения всех вызовов функции `i18n` в проекте с целью последующей передачи ключей в танкер.

После конфигурации следует выполнить команду `tanker pull`, которая затянет необходимые переводы из танкера и разложит по файловой системе рядом с местами использования функции интернационализации.

_Подробнее о конфигурации танкера можно прочитать в [документации tanker-kit](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/tanker-kit/README.md)._

## Заказ переводов

- Создать задачу в очереди [TRANSLATE](https://st.yandex-team.ru/TRANSLATE)
- Заполнить форму
- Указать дедлайн 2 дня
- Дождаться переводов
- Выполнить в корне проекта команду `tanker pull`, которая затянет новые переводы

## Танкер
Ключи и переводы для проектов можно найти в [Танкере](https://tanker.yandex-team.ru/).
