# eslint-kit

Inspired by https://github.com/eslint-kit/eslint-kit

## Установка

```shell
yarn add -D eslint @yandex-travel/eslint-kit@workspace:*
```

## Использование

### Создайте .eslintrc.js

```javascript
const { presets, createConfig } = require('@yandex-travel/eslint-kit');

module.exports = createConfig({
    presets: [
        presets.base(),
        presets.import(),
        presets.typescript({
            // Настройки специфичных правил временно вынесены наверх
            enableTypesPrefixes: true,
            enableRequiredReturn: true,
            enableNoUseBeforeDefine: true,
        }),
        presets.react(),
        presets.node(),
        presets.fsd(),
        presets.nextJs(),
        presets.prettier(),
        presets.effector(),
        presets.extend({
            // ...
        }),
    ],
});
```
