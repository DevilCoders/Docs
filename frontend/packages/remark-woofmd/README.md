# @yandex-int/remark-woofmd

Парсер вики-разметки в AST

## Disclaimer

Это служебный пакет сервиса https://wfaas.yandex-team.ru.
Пожалуйста, не используйте его отдельно

## Установка

```sh
npm install @yandex-int/remark-woofmd
```

## Использование

```js
const { parseWikiMd } = require('@yandex-int/remark-woofmd');

const settings = {}; // Опционально

const ast = parseWikiMd(`*Привет!*`, settings);
```
