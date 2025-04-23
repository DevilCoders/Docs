# Набор хелперов для tanker-kit

Набор вспомогательных утилит для работы с модулем интернализации `@yandex-int/i18n`

Подробнее о [tanker-kit](https://github.yandex-team.ru/lego/tanker-kit/)

## Пример настройки tanker на проекте

Пример подготовленного проекта с настроенной синхронизацией переводов через tanker.

```sh
tree -a -I node_modules example-project

example-project
├── .tanker
│   └── config.js
├── package.json
└── src
    └── components
        └── link
            ├── link.i18n
            │   ├── en.ts
            │   ├── index.ts
            │   └── ru.ts
            └── link.tsx

```

Основная настройка произведена в файле:
.tanker/config.js

## Хелперы

### parser

`ts_parser` – Парсер для поиска ключей в формате ядра `@yandex-int/i18n`.
Работает с файлами типа `ts` или `tsx`.

Подробнее про [Парсинг](https://github.yandex-team.ru/lego/tanker-kit/blob/dev/doc/overview.md#Парсинг)

Подключение в конфиге tanker-kit:

```
const taburetDispatcher = require.resolve('@yandex-int/tanker-helpers/dispatchers/ts_dispatcher.js');

module.exports = function(config) {
    config.parsers.ts = tsParser;
    config.parsers.tsx = tsParser;
};
```

### dispatcher

`ts_dispatcher` – Специальный dispatcher для раскаладки ключей в формате ядра `@yandex-int/i18n`.
И генерации необходимой файловой структуры.

Подробнее про [диспетчеризацию](https://github.yandex-team.ru/lego/tanker-kit/blob/dev/doc/overview.md#Диспетчеризация)

Подключение в конфиге tanker-kit:

```
const taburetDispatcher = require.resolve('@yandex-int/tanker-helpers/dispatchers/ts_dispatcher.js');

module.exports = function(config) {
    config.dispatchers.json = taburetDispatcher;
};
```
