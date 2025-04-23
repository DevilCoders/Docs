# @yandex-lego/storybook-showcase

Общий сторибук с конфигурацией для компонентов написанных в react реализации.

## Использование

1. Добавить зависимость в свой пакет:

```bash
$ npm i -DE @yandex-lego/storybook-showcase --no-package-lock
```

2. Добавить файл конфигурации контекста, по умолчанию это `.config/storybook/context.js` (либо указать через аргумент `--config`):

```js
module.exports = require.context('../../src', true, /\.examples\.tsx$/)
```

3. Добавить скрипты запуска в `package.json`:

```json
{
  "hermione:build": "storybook-showcase build",
  "start": "storybook-showcase start"
}
```

## Кастомизация дефолтного конфига webpack

Надо указать аргумент `--webpackConfig`.  
**Модификаиция производится путем мутирования дефолтного конфига.**

```json
{
  "start": "storybook-showcase start --webpackConfig=\".config/storybook/webpack.config.js\""
}
```

**Пример конфигурации**
```js
module.exports = function ({ config }) {
  config.resolve.alias['~'] = process.cwd();
}
```
