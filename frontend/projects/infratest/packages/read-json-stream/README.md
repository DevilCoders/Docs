# Read JSON from a stream

:warning: Пакет предназначен только для внутреннего использования в реализации Trendbox CI.

Умеет читать JSON из стримов.

## Установка

```console
npm install @yandex-int/trendbox-ci._read-json-stream --registry=https://npm.yandex-team.ru
```

## Использование

```js
const jsonReader = require('@yandex-int/trendbox-ci._read-json-stream');
const json = await jsonReader(process.stdin);
```
