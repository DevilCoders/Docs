vdirectjs
=========

Модуль экспортирует одну функцию `vdirect(keysPath, smsSecretPath)`.

  * `keysPath` — путь к файлу с ключами (обычно `/home/wmi/.vdirectkeys`);
  * `smsSecretPath` — путь к JSON-файлу с секретами для SMS-ссылок.

Функция возвращает объект с 3 методами:

  * `createHashForUidLink(uid, link)` — возвращает подпись для ссылки;
  * `validateHashForUidLink(uid, link, keyHash)` — проверяет подпись для ссылки;
  * `validateHashForSmsLink(link, keyHash, ttl)` — проверяет подпись для SMS-ссылки.

Пример
------

```js
const vdirect = require('vdirectjs')('/home/wmi/.vdirectkeys', '/home/wmi/.smskeys.json');

vdirect.createHashForUidLink('100500', 'http://example.com'); // 'a,SomeHashHere'

vdirect.validateHashForUidLink('100500', 'http://example.com', 'a,SomeHashHere'); // true
vdirect.validateHashForUidLink('100500', 'http://example.org', 'a,SomeHashHere'); // false

// Внутри SomeCipher хранится время создания ts (unix timestamp) и параметр ttl должен быть
// и ссылка валидна если с момента ts прошло меньше ttl секунд.
vdirect.validateHashForSmsLink('http://example.com', 'a,SomeCipher,SomeHash', 86400); // true
```
