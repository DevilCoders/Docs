# bunker-to-js

[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/bunker-to-js/status.svg)](https://drone.yandex-team.ru/project-stub/bunker-to-js)

Выгрузка данных из бункера в [**frozen**](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/isFrozen) JavaScript объект. Поддерживает подключаемые парсеры и миддлвары.

## Install

```
$ npm install --save bunker-to-js
```


## Usage

```js
const BunkerToJs = require('bunker-to-js');

new BunkerToJs({
    api: 'http://bunker-api-dot.yandex.net/v1',
    project: '.bunker-test/api/image'
})
.parse(require('bunker-avatar'))
.then(console.log);
// {
//  'express-bunker.png': '//avatars.yandex.net/get-bunker/381e565d207672cd800f8f0809da212043d91163/normal/381e56.jpg',
//  'screenshot.png': '//avatars.yandex.net/get-bunker/286fa62f1b238cf8d2ea9795029ae2052c762c18/normal/286fa6.png'
// }
```


## API

### BunkerToJs(options)

Поддерживаются все опции [got](https://github.com/sindresorhus/got).

#### api
__Required__
Type: `string`

API-endpoint для бункера.

#### project
__Required__
Type: `string`

Название проекта в бункере. Может быть и конкретной директорией в проекте (например `/photowalks/images`).

__Note__: нельзя указать конкретную ноду с содержимым (см https://github.yandex-team.ru/bunker/api/issues/13).

#### directories
Type: `Boolean`
Default: `false`

Выключает фильтрацию нод, у которых есть дети.

#### freeze
Type: `Boolean`
Default: `true`

Применяет [deep freeze](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) ко
всему дереву. Этот механизм позволяет избежать ошибок, когда объект бункера редактируется по ссылке.
:warning: Не совместимо с кешированием ноды.


### BunkerToJs.then(resolved, [rejected])

Аналог `then` из Promise. При каждом вызове будет создаваться запрос к Бункеру.

В `resolved` передается сгенерированный объект.

В `rejected` передается ошибка при получении данных от бункера или парсинге данных.

### BunkerToJs.use(middleware)

Добавляет `processor` в очередь обработки полученной ноды. Процессор - это функция,
которая будет вызвана для каждой ноды (с контекстом [yabunker](https://github.yandex-team.ru/project-stub/yabunker)).

Пример ноды, которая приходит на обработку

```js
{
	name: 'text-node',
    fullName: '/.bunker-test/api/text-node',
    version: 1,
    isDeleted: false,
    mime: {
       type: 'text',
       subtype: 'plain',
       suffix: undefined,
       parameters: {}
    },
    saveDate: '2014-08-06T10:44:54.000Z',
    publishDate: null,
    relative: 'text-node'
}
```

Дополнительно можно устанавливать 2 свойства:

- ``.content`` - контент. Пример, [bunker-cat](https://github.yandex-team.ru/project-stub/bunker-cat) или [bunker-avatar](https://github.yandex-team.ru/project-stub/bunker-avatar).
- ``.skip`` - пропуск ноды при обработке. Пример, [bunker-filter](https://github.yandex-team.ru/project-stub/bunker-filter).

По окончанию обрабоки процессор может вызвать `next`:

 * `next()` — без параметра — передать ноду дальше.
 * `next(Error)` — сообщить об ошибке обработки ноды.

Пример (выводит все ноды в консоль):

```js
BunkerToJs({
    api: 'http://bunker-api-dot.yandex.net/v1',
    project: '.bunker-test/api/image'
})
    .use((node, cb) => {
        console.log(node);
        cb();
    });
```

### BunkerToJs.parse(middleware)

Аналог `bunker.use`, за исключением того, что парсер будет пропущен, если у ноды уже установлено свойство `content`.
Порядок подключения парсеров важен — если подключить [bunker-cat](https://github.yandex-team.ru/project-stub/bunker-cat) первым, то он выкачает содержимое для ноды и остальные парсеры не применятся.

### Parsers

#### BunkerToJs.filter

Процессор, помогающий фильтровать ноды.
```js
const BunkerToJs = require('bunker-to-js');

new BunkerToJs()
    .use(BunkerToJs.filter.hidden)
    .use(BunkerToJs.filter.empty);
```

##### filter.hidden

Отфильтровывает скрытые ноды или ноды, находящиеся в скрытых папках (начинающихся с `.`).

##### filter.empty

Отфильтровывает ноды, у которых нет контента (обычно, такие ноды не проходят по `isDeleted === false`).

#### BunkerToJs.avatar

Парсер ссылок на Аватариницу из mime ноды Бункера. Испольуется в bunker-to-js.

Матчится на все ноды с mime-типом image/svg+xml и присутствующим avatar-href в mime.
```js
const BunkerToJs = require('bunker-to-js');
new BunkerToJs().parse(BunkerToJs.avatar);
````

##### bunker-avatar.withProtocol

То же самое, только оставляет протокол в покое.

#### BunkerToJs.tjson

Функция-парсер, которая запишет результат `new TJSON(JSON.parse(content))` от запрошенного содержимого ноды.
Матчится на все ноды с mime-типом `application/json; schema="bunker:/.schema/tjson#"`.

```js
const BunkerToJs = require('bunker-to-js');
BunkerToJs().parse(BunkerToJs.tsjon);
```

API для TJSON описано в репозитории модуля [tjson](https://github.yandex-team.ru/project-stub/tjson).

#### BunkerToJs.json

Функция парсер, которая запишет результат `JSON.parse` от запрошенного содержимого ноды. Матчится на все ноды с
mime-типом `application/json`.

```js
const BunkerToJs = require('bunker-to-js');
BunkerToJs().parse(BunkerToJs.json);
```

#### BunkerToJs.cat

Функция парсер, которая запишет запрошенное содержимое ноды.

```js
const BunkerToJs = require('bunker-to-js');
BunkerToJs().parse(BunkerToJs.cat);
```


## License

MIT © [Vsevolod Strukchinsky](http://staff.yandex-team.ru/floatdrop)
