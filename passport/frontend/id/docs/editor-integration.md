## Настройка линтеров в редакторе

### VSCode

Для начала необходимо установить следующие расширения:

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) — расширение для проверки JS- и TS-файлов.
- [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint) — расширение для проверки файлов стилей.
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) — расширение для форматирования файлов.
- [Format Code Action](https://marketplace.visualstudio.com/items?itemName=rohit-gohri.format-code-action) — добавляет в VSCode действие форматирования документа при сохранении (в VSCode появилась возможность запускать при сохранении разные действия в определенной последовательности, но из коробки их практически нет).
- [monorepo-workspace](https://marketplace.visualstudio.com/items?itemName=folke.vscode-monorepo-workspace) — расширение предоставляет удобный способ открыть в одном редакторе разные рабочие области в монорепе. В первую очередь это необходимо для `prettier` и `eslint`, так как эти расширения могут некорректно подключать `.prettierignore` и `.eslintignore` и резолвят их из корня монорепы.

После установки расширений можно в файле конфигурации указать следующие параметры:

```json
{
  "prettier.requireConfig": true,
  "prettier.resolveGlobalModules": false,
  "prettier.useEditorConfig": true,

  "eslint.alwaysShowStatus": true,
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"],
  "eslint.debug": true,

  "stylelint.reportNeedlessDisables": true,
  "stylelint.reportInvalidScopeDisables": true,

  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.formatOnSave": false,
    "editor.codeActionsOnSave": ["source.formatDocument", "source.fixAll.eslint"]
  },
  "[typescript]": {
    "editor.formatOnSave": false,
    "editor.codeActionsOnSave": ["source.formatDocument", "source.fixAll.eslint"]
  },
  "[typescriptreact]": {
    "editor.formatOnSave": false,
    "editor.codeActionsOnSave": ["source.formatDocument", "source.fixAll.eslint"]
  },
  "[css]": {
    "editor.formatOnSave": false,
    "editor.codeActionsOnSave": ["source.formatDocument", "source.fixAll.stylelint"]
  }
}
```

После изменения настроек желательно перезагрузить редактор и все должно работать. При сохранении файла сначала будет запускаться форматирование с помощью `prettier`, а потом исправление правил, которые можно исправить с помощью `stylelint` или `eslint` в зависимости от расширения.
