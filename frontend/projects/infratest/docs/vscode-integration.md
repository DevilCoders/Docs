# Интеграция с VS Code

## Работа плагина [ESLint](https://github.com/Microsoft/vscode-eslint)

```json5
{
    "eslint.options": {
        "resolvePluginsRelativeTo": "./node_modules/@yandex-int/eslint-config-infratest"
    },
}
```

> :book: Совет. Эти настройки лучше указывать на уровне воркспейса (`./.vscode/settings.json`), чтобы не влиять на другие проекты.

### Если открыта вся монорепа, а не отдельный пакет или сервис

По умолчанию плагин не работает с монорепозиториями, в которых сам линтер (`eslint`) установлен в каждом пакете, а не в корневом `package.json`. Эту поддержку нужно включать вручную.

```json5
{
    "eslint.packageManager": "pnpm",
    "eslint.workingDirectories": [{ "mode": "auto" }]
}
```
