# Yandex Wiki API Node.JS Client

Node.js клиент для [Yandex Wiki REST API](https://wiki.yandex-team.ru/wiki/dev/api/autodocs/).

## Установка

```shell
npm install --save --registry=http://npm.yandex-team.ru/ @yandex-int/si.ci.yawiki
```

## Использование

```js
const createYaWikiClient = require('@yandex-int/si.ci.yawiki');
const yaWiki = createYaWikiClient({ token: '******' });

yaWiki.getPageSource('/your-page')
    .then(console.log)
    .catch(console.error);
```

Кроме того, есть CLI: [`@yandex-int/si.ci.yawiki-cli`](../yawiki-cli).

## Отладка

Включить отладочный вывод для библиотеки можно через переменную окружения `DEBUG`:

```bash
DEBUG=yawiki node your-app.js
```
