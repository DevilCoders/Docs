# yamurmurhash3 [![Build Status][drone-image]][drone-url]

JavaScript реализация MurmurHash3.

За основу взята реализация функция `murmurHash3.x86.hash32` из библиотеки [`MurmurHash3js`](https://github.com/pid/murmurHash3js)

Изменен способ получение числа из строки. Используется алгоритм, аналогичный методу `buf.readInt32BE()`, в `MurmurHash3js` реализован аналог метода `buf.readInt32LE()`. Как показывают тесты, эта реализация быстрее более чем в два раза.

## Install

```bash
npm install --save yamurmurhash3
```

## Usage
```js
var murmurHash3 = require('yamurmurhash3');

murmurHash3('1234567890', 123); //1318753088
```

## API

### murmurHash3(key, seed)

Возвращает хэш по ключ `key` с солью `seed`.

#### key
Type: `String`

Ключ, по которому требуется получить хэш

#### seed
Type: `Number`

Соль для хэш-функции. Число больше нуля.

## Tests
```bash
npm i
npm test
```

## Benchmark
```bash
npm i
node benchmark
```

Результаты на моем ноутбуке:
```
with remainder 0 x 7,574,796 ops/sec ±1.39% (98 runs sampled)
with remainder 1 x 7,164,181 ops/sec ±0.40% (97 runs sampled)
with remainder 2 x 7,145,936 ops/sec ±0.41% (99 runs sampled)
with remainder 3 x 7,086,362 ops/sec ±0.77% (99 runs sampled)
```

## Related
* [Модуль `MurmurHash3js`](https://github.com/pid/murmurHash3js)
* [MurmurHash](https://en.wikipedia.org/wiki/MurmurHash)

# License
MIT

[drone-url]: https://drone.yandex-team.ru/toolbox/yamurmurhash3
[drone-image]: https://drone.yandex-team.ru/api/badges/toolbox/yamurmurhash3/status.svg
