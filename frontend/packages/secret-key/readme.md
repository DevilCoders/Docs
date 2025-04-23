# secret-key [![Build Status](http://drone.haze.yandex.net/api/badge/github.yandex-team.ru/project-stub/secret-key/status.svg?branch=master&style=flat)](http://drone.haze.yandex.net/github.yandex-team.ru/project-stub/secret-key)

Библиотека для работы с secret-key.


## v2(options)

```js
var v2 = require('secret-key/v2');

v2({ uid: '1', yandexuid: '' });
// => throws error 'options.salt is required for v2 keys'

v2({ salt: 'hash', uid: '1', yandexuid: '' });
// => 'e6479b5ec6b4cea367cd5e78bf2184b5e69e445f:1418651608569'

v2.isValid('e6479b5ec6b4cea367cd5e78bf2184b5e69e445f:1418651608569', { salt: 'hash', uid: '1', yandexuid: '' });
// => true or false
```

Генерация HMAC-SHA1 версии с солью.

Подробнее можно прочитать тут:

 * https://beta.wiki.yandex-team.ru/security/For/developers/csrf-token/#kakgenerirovatiproverjattoken

###### options

 * `salt` - соль для hmac-sha1 (__при отсутствии будет выброшено исключение__).
 * `uid` - идентификатор пользователя (например из blackbox). Если пользователь не авторизирован, то по умолчанию используется `0`.
 * `yandexuid` - значение coockie yandexuid.
 * `lifetime` - время жизни (в миллисекундах). По умолчанию __один день__.
 * `timestamp` - дата генерации ключа (в миллисекундах). По умолчанию Date.now().

#### v2.isValid(key, options)

Проверяет валидность ключа `key` по переданным `options` (см. выше).

## v1([options])

```js
var v1 = require('secret-key/v1');

v1({ uid: '1', yandexuid: '' });
// => 'u05ffa9b0b0c034b232b0ba09680c2c9d'

v1.isValid('u05ffa9b0b0c034b232b0ba09680c2c9d', { uid: '1', yandexuid: '' });
// => true or false
```

Генерация MD5 версии токена. Подробнее можно прочитать тут:

 * http://doc.yandex-team.ru/XScript5/interface-developer-guide/concepts/secret-key.xml
 * https://github.yandex-team.ru/InfraComponents/xscript-yandex/blob/master/util.cpp

Ключ действителен в течение текущих и следующих суток с момента генерации.

###### options

 * `uid` - идентификатор пользователя (например из blackbox). Если пользователь не авторизирован, то по умолчанию используется `0`.
 * `yandexuid` - значение coockie yandexuid.
 * `days` - количество дней от 1 January 1970 00:00:00 UTC.
 * `salt` - соль для добавления в ключ, по умолчанию используется пустая строка.

#### v1.isValid(key, [options])

Проверяет валидность ключа `key` по переданным `options` (см. выше).
