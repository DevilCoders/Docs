# yandex-tjson

Фасад для работы с TJSON.

#### [Документация для версии 1.x](https://github.yandex-team.ru/project-stub/tjson/tree/v1.5.1#tjson-)

## Usage

```js
// npm i tjson

var TJSON = require('yandex-tjson');
var i18n = new TJSON(require('./example.json'));

var ru = i18n.lang('ru');
var index = ru.keyset('index');

index.get('worng');                                 // undefined
index.get('right');                                 // 'Правильно'
'10 ' + index.get('points', 10);                    // '10 баллов'

index.get('maybe') || 'default';                    // `default`

i18n.languages();                                  // ['ru']
i18n.keysets('ru');                                // ['index']

ru.keysets();                                      // ['index']
ru.keys('index');                                  // ['right', 'points']

index.keys();                                      // ['right', 'points']
```

## API

### TJSON(json)

Возвращает объект-обертку над переводами.

#### tjson.lang(language)

Возвращает TJSON с выбранным языком.

#### tjson.keyset(keyset)

Возвращает TJSON с выбранным кейсетом.

#### tjson.get(key, [count])

Возвращает значение ключа в выбранном кейсете для выбранного языка. Если ключ является числительным, то будет возвращено значение относительно `count`.

`get` возвращает `undefined` в следующих ситуациях:

 * Если `keyset` или `lang` не выбраны
 * Если `keyset` нет в выбранном `lang`
 * Если ключа `key` нет в выбранном `keyset` для выбранного `lang`

#### tjson.merge(json)

Добавляет к текущим переводам новые из `json`. При совпадении старые будут переопределены.

#### tjson.languages()

Возвращает массив языков.

#### tjson.keysets([lang])

Возвращает массив кейсетов для языка `lang` (по умолчанию берется выбранный язык).

#### tjson.keys([keyset], [lang])

Возвращает массив ключей для языка `lang` и кейсета `keyset` (по умолчанию берется выбранный язык и кейсет).

#### tjson.key(key, [keyset], [lang])

Возвращает представление ключа `key` для языка `lang` и кейсета `keyset` (по умолчанию берется выбранный язык и кейсет).

На данный момент это объект с полями:

 * `isPlural` - является ли ключ числительным (`Boolean`)
 * `form` - форма ключа по умолчанию (`String` или `undefined`)
 * `one`, `some`, `many` - формы ключа для числительных (`String` или `undefined`)
 * `none` - форма ключа для числетильных (если число равно 0) (`String` или `undefined`)
