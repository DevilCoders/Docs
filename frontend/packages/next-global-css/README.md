# Next.js + Global css

![npm version](https://badger.yandex-team.ru/npm/@yandex-int/next-global-css/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/next-global-css/owner.svg)

Плагин для Next.js, который позволяет в next проекте подключать глобальные стили не только в \_app

## Установка

```sh
npm install --save @yandex-int/next-global-css
```

## Использование

Создайте файл `next.config.js` в вашем проекте

```javascript
const nextGlobalCss = require('@yandex-int/next-global-css');

const withGlobalCss = nextGlobalCss({
    src: path.resolve(__dirname, 'src'),
});

module.exports = withGlobalCss({
  // ...проектные настройки next.js
});
```

## Совместимость

Для работы необходим Next.js >= v9.5
