# Что это и зачем

Cм. https://st.yandex-team.ru/HOME-56794. Для проверки подстановок `[% expression %]` в html-представлениях потребовалось научить ESLint парсить *.html.  Сейчас парсер умеет извлекать массив подстановок, правильно обрабатывая html-комментарии.

# Настройка в проекте

После `cd PROJ/ && npm i -D morda-template-eslint-parser` в настройках eslint (например, `.eslintrc.js`) добавляем

```javascript
{
    ...,
    parser: 'morda-template-eslint-parser',
    parserOptions: {
        ...,
        extraFileExtensions: ['.html'],
        ...
    },
    rules: {
        // JS/TS правила
    },
    overrides: [
        {
            files: ['*.html'],
            rules: {
                // правила для view.html-шаблонов
            }
        }
    ]
    ...
}
```

Если Вы уже используете кастомный парсер, например `@typescript-eslint/parser`, то его нужно пробросить в конфиге
```javascript
{
    ...,
    parser: 'morda-template-eslint-parser',
    parserOptions: {
        ...,
        parser: '@typescript-eslint/parser',
        extraFileExtensions: ['.html'],
        ...
    },
    ...
}
```

В VS Code включить ESLint на html-шаблонах можно, добавив в `proj/.vscode/settings.json`
```json
{
    ...,
    "eslint.validate": ["javascript", "typescript", "html"],
    ...
}
```

