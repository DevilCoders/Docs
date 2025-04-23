@yandex-int/lru-cache
=

### Использование:
```js
const { LruCache } = require('@yandex-int/lru-cache');

const cache = new LruCache(300); // 300 - максимальное количество ключей

cache.set('key', 42);
cache.get('key'); // => 42
```

### Демонстрация LRU:
```js
const { LruCache } = require('@yandex-int/lru-cache');

const cache = new LruCache(2);

cache.set('key1', 1);
cache.set('key2', 2);

// key1 был использован, стал более используемым чем key2
cache.get('key1'); // 1

// Добавляю третий ключ, при максимальном количестве - 2
cache.set('key3', 3);

// key2 был удален при установке key3, потому что используется реже чем key1
cache.get('key2'); // undefined
```
