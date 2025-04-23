# log-cleaner

Поставляется as is, без гарантий.

## Установка

```bash
npm i --save-dev --save-exact @yandex-int/log-cleaner --registry https://npm.yandex-team.ru
```

## Использование
```javascript
const logCleaner = require('@yandex-int/log-cleaner');

await logCleaner.clean(options);
```

## Опции

### `logDir`
Абсолютный путь к директории с логами, обязательный параметр.

Подразумевается следующая структура, удаляются файлы из поддиректорий.
```
/Users/flack/.yandex-int/logs
├── calc-metrics-daemon
│   ├── YTNmYTc4MC9jaHJvbWUtZGVza3RvcCwxNTUxMTE2OTM0MDg0LCw=_2019-02-25T17:49:23.217527Z
│   ├── YTNmYTc4MC9jaHJvbWUtZGVza3RvcCwxNTUxMTE2OTM0MDg0LCw=_2019-02-25T17:49:35.437200Z
├── clickdaemon
│   ├── access-49534.log
│   ├── access-49550.log
└── rr
    ├── current-report-renderer_custom-49479
    ├── current-report-renderer_custom-49501
```

### `maxFiles`

Удаляет самые старые файлы, пока общее количество файлов в директории с логами не уложится в указанный лимит.

По умолчанию выключена.

### `keepFilesPerDir`

При указании параметра в каждой поддиректории, независимо от значения других опций, будут сохранены последние N файлов.

Например, если `keepFilesPerDir` имеет значение `2`, то в каждой поддиректории будут сохранены по два последних файла, даже если их суммарное количество превышает `maxFiles`.

По умолчанию файлы не сохраняются.

### `maxDirSize`

Удаляет самые старые файлы, пока общий размер директории не уложится в указанный лимит.

По умолчанию выключена.

:warning: Параметр `maxDirSize` имеет приоритет перед `maxFiles`.

:warning: При указании `keepFilesPerDir` итоговый размер директории может быть больше запрошенного. 
