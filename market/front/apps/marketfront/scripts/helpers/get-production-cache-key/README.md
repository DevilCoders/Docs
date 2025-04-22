# Как сбросить кэш резолвера в проде

## кратко (для FAPI ./api)

#### 1. нужно самому собрать значение возвращаемое resolver cache.key

нужны параметры резолвера, на выходе получим строка - по сути нужно выполнить
[эту](https://github.yandex-team.ru/market/marketfront/blob/b260327e29de8bcbc2a0372f75796196b02124cb/src/resolvers/search/resolveGoEntryPointsCachedByRegionId.js#L144)
функцию, но с нужными параметрами.

должно получиться что-то такое `resolveGoEntryPointsCachedByRegionId-213`

#### 2. далее передаем скрипту название резолвера и значение из пункта 1 и получаем ключ кэша

```
node ./get-production-api-cache-key.js \
resolveGoEntryPointsCachedByRegionId \
resolveGoEntryPointsCachedByRegionId-213

3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w==
```

#### 3. подключаемся на public

```
$ ssh public.market.yandex.net
```

#### 4. подключаемся к memcached

актуальный хост/порт мемкэша должен быть в [production/node.js](https://github.yandex-team.ru/market/marketfront/blob/af38e24af4b7cd9f969388602d5554f3df0a0008/api/configs/production/node.js#L18), но скорее всего он не поменяется

У мемкэша [простой текстовый протокол](https://github.com/memcached/memcached/blob/master/doc/protocol.txt#L323), поэтому для подключения подойдет tenet или nc

```
$ telnet front-cache.vs.market.yandex.net 11226
Trying 2a02:6b8:0:3400::56b...
Connected to front-cache.vs.market.yandex.net.
Escape character is '^]'.
```

#### 5. проверяем что такой ключ есть

```
get 3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w==

// в ответ должно быть так
VALUE 3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w== 2 48
{"result":{"searchIntents":[]},"collections":{}}
END

// если отвечает так значит ключа нет
END
```

#### 6. удаляем ключ

```
delete 3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w==
DELETED

// Если ключа нет
NOT_FOUND
```

#### 9. эта успех

## долго и нудно выясняем как собирается ключ кэша

### 1. в резолвере мы можем добавить функцию для генерации ключа

например, [так](https://github.yandex-team.ru/market/marketfront/blob/b260327e29de8bcbc2a0372f75796196b02124cb/src/resolvers/search/resolveGoEntryPointsCachedByRegionId.js#L144):

```js
// ...
}, {
    name: 'resolveGoEntryPointsCachedByRegionId',
    cache: {
        ttl: 60 * 60, // 60 минут
        level: 'shared',
        key: (ctx, params) => {
            const {regionId} = params;
            return `resolveGoEntryPointsCachedByRegionId-${regionId}`;
        },
    },
});
```
Дальше происходит неконтролируемая магия по генерации ключа кэша и кэшированию.

"Неконтролируемая" потому что со стороны резолвера мы не можем никак на это повлиять

### 2. Дальше в mandrel.createResolver [добавляется кэширование](https://github.yandex-team.ru/market/monomarket/blob/master/lib/lib/mandrel/src/resolver/index.ts#L155-L180)

нас больше всего интересует эта [строка](https://github.yandex-team.ru/market/monomarket/blob/master/lib/lib/mandrel/src/resolver/index.ts#L163)

```js
 let underline = cachelib.create(cache.level, _settings.name, cache.capacity);
```

А точнее два первых параметра:

- первый `cache.level` - для резолвера из 1 пункта он будет равен `shared`
- второй `_settings.name` - это имя резолвера, name из 1 пункта будет равен `resolveGoEntryPointsCachedByRegionId`

### 3. Дальше начинает работать @yandex-market/cache

[Функция create](https://github.yandex-team.ru/market/cache/blob/master/src/index.ts#L58-L92)

__ используем [shared.create](https://github.yandex-team.ru/market/cache/blob/master/src/index.ts#L680) для level =shared

__ передаем внутрь [shared.create](https://github.yandex-team.ru/market/cache/blob/master/src/index.ts#L73) id, он будет равен названию резолвера - `resolveGoEntryPointsCachedByRegionId`

__ и при кэшировании резолвера используется node-hashit, чтобы сделать хэш от ключа, который вернула функция key из резолвера

__ остается посмотреть [shared create](https://github.yandex-team.ru/market/cache/blob/master/src/shared.ts#L56)

```js

const prefix = `${generation}|${_id || id++}|`;

return ( ... ) => {
    ...
    return impl(fn, space, prefix + key, ttl);
}
```

тут генерируется итоговое значение ключа, который будет складываться в memcache

### ключи в конфигах

нам нужен только generation из [production/node.js](https://github.yandex-team.ru/market/marketfront/blob/af38e24af4b7cd9f969388602d5554f3df0a0008/api/configs/production/node.js#L70)

Сейчас (31.08.2021) он равен `3`

### как собирается ключ в нескольких строчках

```js
// из конфига
const generation = '3';

// название резолвера из resolver settings
const id = 'resolveGoEntryPointsCachedByRegionId';

// функция генерации ключа из резолвера, cache.key
const keyFn = (ctx, params) => {
    const {regionId} = params;
    return `resolveGoEntryPointsCachedByRegionId-${regionId}`;
};

// опции для генерации ключа из yandex-market/cache
const HASHIT_OPTIONS = {
    algorithm: 'md5',
    outputEncoding: 'base64',
    sortArrays: true,
};

const {hashit} = require('hashit');

// рхэш делается только для того что вернул cache.key из резолвера
const keyHash = hashit(keyFn(ctx, {regionId: 213}), HASHIT_OPTIONS).toString();

// и собираем уже ключ
const memcacheKey = `${generation}|${id}|${keyHash}`;

// В итоге получим такое 3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w==


```

### взаимодействие с memcache

Сервера можно найти в том же [production/node.js](https://github.yandex-team.ru/market/marketfront/blob/af38e24af4b7cd9f969388602d5554f3df0a0008/api/configs/production/node.js#L18)

У мемкэша [простой текстовый протокол](https://github.com/memcached/memcached/blob/master/doc/protocol.txt#L323), поэтому для подключения подойдет tenet или nc

__ подключаемся к паблику

```
ssh public.market.yandex.net
```

__ подключаемся к мемкешу

```
$ telnet front-cache.vs.market.yandex.net 11226
Trying 2a02:6b8:0:3400::56b...
Connected to front-cache.vs.market.yandex.net.
Escape character is '^]'.
```

__ проверяем что ключ есть

```
get 3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w==

// в ответ должно быть так
VALUE 3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w== 2 48
{"result":{"searchIntents":[]},"collections":{}}
END

// если отвечает так значит ключа нет
END
```

__ удаляем ключ

```
delete 3|resolveGoEntryPointsCachedByRegionId|9CaWuTViXfDRk3+pCKO+9w==
DELETED

// Если ключа нет
NOT_FOUND
```

__ успех!!!1



