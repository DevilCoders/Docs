![bunker_sc2_rend1](https://github.yandex-team.ru/github-enterprise-assets/0000/1193/0000/0731/1023efee-3ffa-11e4-8fdd-2f2e5bf43f71.png)

---

[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/express-bunker/status.svg)](https://drone.yandex-team.ru/project-stub/express-bunker)

Миддлвара для загрузки содержимого проекта из [Бункера](https://beta.wiki.yandex-team.ru/verstka/tools/bunker/) в приложение.

## Installation

```
npm install express-bunker --save
```

## Usage

```js
const app = require('express')();
const bunker = require('express-bunker');

const bunkerMiddleware = bunker({
    api: 'http://bunker-api-dot.yandex.net/v1',
    project: '.bunker-test/api/image',
    version: 'stable'
});

app.use(bunkerMiddleware);

app.get('/', function(req, res) {
	res.send(`<img src="${req.bunker['express-bunker.png']}" />`);
});

app.listen(8080);
```

## API

### Bunker([options](#options))

Поддерживаются все опции [got](https://github.com/sindresorhus/got).

### options

#### api
__Required__
Type: `string`

API-endpoint для бункера.

#### project
__Required__
Type: `string`

Название проекта в бункере. Может быть и конкретной директорией в проекте (например `/photowalks/images`).

__Note__: нельзя указать конкретную ноду с содержимым (см https://github.yandex-team.ru/bunker/api/issues/13).

#### version
Type: `string`
Default: `latest`

Версия нод в бункере. Популярные значения: `stable`, `latest`.

#### updateInterval
Type: `Number`
Default: `5000`

Как часто обновлять содержимое из Бункера (`0` – никогда).

#### directories
Type: `Boolean`
Default: `true`

Выгружать контент у директории (_не детей, а контент_).

#### cache
Type: `Boolean`
Default: `true`

Подключать ли [`bunker-cache`](http://github.yandex-team.ru/project-stub/bunker-cache).

#### freeze
Type: `Boolean`
Default: `false`

Применять ли [deep freeze](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
к объекту бункера. Этот механизм позволяет избежать ошибок, когда объект бункера редактируется по ссылке.
__Внимание!__ Опция не совместима с bunker-cache и требует `cache: false`, иначе будет проигнорирована.

#### parsers
Type: `Array`
Default: [[`BunkerToJs.filter.hidden`](https://github.yandex-team.ru/project-stub/bunker-to-js/#filterhidden),
[`BunkerToJs.filter.empty`](https://github.yandex-team.ru/project-stub/bunker-to-js/#filterempty),
[`BunkerToJs.avatar`](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojsavatar),
[`BunkerToJs.tjson`](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojstjson),
[`BunkerToJs.json`](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojsjson),
[`BunkerToJs.cat`](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojscat)]

Список парсеров, подключаемых к [`bunker-to-js`](https://github.yandex-team.ru/project-stub/bunker-to-js/#parsers).

#### propertyName
Type: `string`
Default: `bunker`

Имя свойства в которое сохранять выгруженные данные (например `bunker`, `deep.property`).


## Related

Процессоры:

* [bunker-cache](https://github.yandex-team.ru/project-stub/bunker-cache)
* [bunker-filter](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojsfilter)

Парсеры:

* [BunkerToJs.cat](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojscat)
* [BunkerToJs.json](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojsjson)
* [BunkerToJs.tjson](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojstjson)
* [BunkerToJs.avatar](https://github.yandex-team.ru/project-stub/bunker-to-js/#bunkertojsavatar)

Полезное:

* [wrap-middleware](https://github.com/floatdrop/wrap-middleware) – для постпроцессинга
* [ignore-middleware-error](https://github.com/floatdrop/ignore-middleware-error) - игнорируем ошибки от бункера
