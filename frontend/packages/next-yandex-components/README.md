# Next.js + Yandex Components

![npm version](https://badger.yandex-team.ru/npm/@yandex-int/next-yandex-components/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/next-yandex-components/owner.svg)

Плагин для Next.js, с помощью которого компилируются компоненты, например, из следующих пакетов:

- @yandex/ui
- @yandex-int/edu-components
- video-components
- @yandex-lego/components
- @yandex-int/serp-components
- @yandex-int/mushrooms-components

Компоненты поставляются с импортами CSS и других ресурсов, поэтому их необходимо компилировать на стороне потребителя.

## Установка

```sh
npm install --save-dev @yandex-int/next-yandex-components
```

## Использование

Создайте файл `next.config.js` в вашем проекте

```javascript
const nextYandexComponents = require('@yandex-int/next-yandex-components');

const withYandexComponents = nextYandexComponents(['@yandex-lego/components']);

module.exports = withYandexComponents({
  /* Next.js config options here */
});
```

## Совместимость с Next.js

| Next.js | @yandex-int/next-yandex-components |
| ------- | ---------------------------------- |
| < 9.4   | 0.1.5                              |
| >= 9.5  | 1.x.x                              |
