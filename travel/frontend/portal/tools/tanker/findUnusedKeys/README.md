Статический анализатор, который ищет неиспользуемые ключи и кейсеты из Танкера.

[Babel Plugin Handbook (ru)](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/ru/plugin-handbook.md#toc-babel-traverse)

Выводит кейсеты и ключи, использование которых не нашлось в папках `src` и `server`.

Для `unsafeDynamicKeyset` и `i18nBlock[type]()` считаем что кейсет используется целиком.

## find-unused-keys

Поиск неиспользуемых в коде текущей ветки ключей из танкера.

```
npm run i18n:find-unused-keys
```

Скачивает актуальные ключи из мастера танкера и ищет все использования ключей в коде для текущей ветки.
Создает html отчет с ключами и кейсетами, которые не используются.

```
/tmp/unused-tanker-report.html
```

## find-used-keys

Ищет все использования ключей танкера в коде для текущей ветки.

```
npm run i18n:find-used-keys
```

Создает отчет в JSON

```
/tmp/used-tanker-keys.json
```

## delta-used-keys

Нужно доставить в папку `/tmp` файл `used-tanker-keys.previous.json` с предыдущей версией отчета для find-used-keys.
А также запустить find-used-keys, чтобы создать актуальный отчет.
Таска выведет ключи, которые были в старом отчете и пропали в новом.

```
npm run i18n:delta-used-keys
```

Создает html отчет с ключами, которые больше не используются в ветке.
