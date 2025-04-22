# qr2

> API для работы с `https://disk.yandex.net/qr/`.

## Установка

```shell
npm install @yandex-int/si.ci.qr2
```

## Использование

```js
const qr = require('@yandex-int/si.ci.qr2');

const url = qr.formatUrl('text'); // -> https://disk.yandex.net/qr/?text=text
```

## API

### .formatUrl(text, [options]) -> string

Возвращает ссылку на QR-код.

#### text

Текст, кодируемый в QR-коде.

* Type: `string`

#### options

Опции для персонализации QR-кода. Подробнее в интерфейсе [`QrOptions`](./src/qr.ts).
