# @yandex-market/mbo-linters

Общие конфиги MBO для prettier, eslint и stylelint.

## Установка

```bash
npm i --save-dev --registry=https://npm.yandex-team.ru @yandex-market/mbo-linters
```

## Подключение

### Prettier

Файл `.prettierrc.js` в корне проекта

```js
module.exports = require('@yandex-market/mbo-linters/prettier');
```

### TSLint

NOTE: tslint should be migrated to eslint, see [ESLINT.md](ESLINT.md)

**tslint.json**:

```json
{
  "extends": "@yandex-market/mbo-linters/tslint"
}
```

### Stylelint

**package.json**:

```json
  "stylelint": {
    "extends": "@yandex-market/mbo-linters/stylelint"
  }
```
