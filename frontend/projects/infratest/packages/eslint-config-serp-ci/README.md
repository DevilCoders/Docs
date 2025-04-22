# eslint-config-serp-ci

Конфиг для [ESLint](http://eslint.org/).

## Установка

```bash
npm install @yandex-int/eslint-config-serp-ci --registry=https://npm.yandex-team.ru
```

## Использование

* Добавить в корень проекта файл `.eslintrc.js`:

```js
module.exports = {
    root: true,
    extends: '@yandex-int/eslint-config-serp-ci'
};
```
