# HOW TO TRANSITION FROM TSLINT TO ESLINT

![npm version](https://badger.yandex-team.ru/npm/@yandex-market/mbo-linters/version.svg)

Набор ESLint правил для проектов MBO, в которых используются TypeScript и React.

Основан на конфигах [airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb) и [@typescript-eslint/recommended](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin), совместим с [Prettier](https://prettier.io).

## Установка

```bash
npm install --save-dev eslint prettier typescript @yandex-market/mbo-linters
```

## Использование

Унаследуйте конфигурацию `eslint` из `@yandex-market/mbo-linters` и укажите путь до `tsconfig.json` проекта:

`.eslintrc.js`

```js
const path = require('path');
const tsConfigDir = __dirname;

const jsExtensions = ['.js'];
const tsExtensions = ['.ts', '.tsx', '.d.ts'];
const assetsExtensions = ['jpg', 'jpeg', 'png', 'svg', 'css', 'scss', 'json'];

module.exports = {
  extends: ['./node_modules/@yandex-market/mbo-linters'],
  env: {
    jest: true,
    node: true,
    browser: true
  },
  parserOptions: {
    project: path.join(tsConfigDir, 'tsconfig.json')
  },
  settings: {
    react: { version: 'detect' },
    'import/resolver': {
      typescript: {
        directory: tsConfigDir,
      },
    },
    'import/extensions': jsExtensions.concat(tsExtensions),
    'import/parsers': { '@typescript-eslint/parser': tsExtensions },
    'import/ignore': ['node_modules', `\\.(${assetsExtensions.join('|')})$`],
  }
};
```

## Настройки EditorConfig

`.editorconfig`

```editorconfig
root = true

[*]
charset = utf-8
indent_size = 2
end_of_line = lf
indent_style = space
max_line_length = 120
insert_final_newline = true
trim_trailing_whitespace = true

[*.md]
trim_trailing_whitespace = false
```

Настройте Prettier:

`.prettierrc.js`

```javascript
module.exports = require("@yandex-market/mbo-linters/prettier");
```

При этом prettier унаследует следующие настройки:

```json
{
  "printWidth": 120,
  "trailingComma": "es5",
  "semi": true,
  "singleQuote": true,
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "arrowParens": "avoid",
  "useTabs": false,
  "tabWidth": 2
}
```

## Переход

Перед использованием нужно отформатировать весь существующий код.
Для этого необходимо включить в `scripts` файла `package.json` следующие скрипты:

```json
"lint": "eslint --ext .ts,.tsx,.json src/",
"lint:fix": "eslint --ext .ts,.tsx,.json src/ --fix",
```

а затем выполнить команду `npm run lint:fix`. Данная команда можеть исправит часть ошибок статической проверки синтаксиса автоматически. Оставшуюся часть ошибок необходимо исправить вручную.

С момента перехода на `eslint` необходимо удалить npm-зависимости `tslint` и конфигурационные файлы `tslint*.json`.

## VSCode

По умолчанию, плагин ESLint для VSCode проверяет только файлы с расширениями `.js` и `.jsx`.
Вам необходимо вручную включить проверку файлов `.ts` и `.tsx` в настройках IDE:

`settings.json`

```json
"eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "typescript",
      "autoFix": true
    },
    {
      "language": "typescriptreact",
      "autoFix": true
    }
]
```
