# yabunker 

[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/yabunker/status.svg)](https://drone.yandex-team.ru/project-stub/yabunker)

Простая обертка для хождения в API Бункера. Используется в [express-bunker](https://github.yandex-team.ru/project-stub/express-bunker).

```js
var Bunker = require('yabunker');
var bunker = Bunker({
    api: 'http://bunker-api-dot.yandex.net/v1'
});

bunker.cat('/.bunker-test/api/text-node').then(console.log);
bunker.ls('/.bunker-test/api').then(console.log);
bunker.tree('/.bunker-test/api').then(console.log);
```

# API

## Bunker(options)

Создает объект Bunker.

### options

Поддерживаются все опции [got](https://github.com/sindresorhus/got#goturl-options).

#### api
__Required__
Type: `string`  

Адрес [API v1](https://github.yandex-team.ru/bunker/api#api-v1-current-stable):

 * `http://bunker-api.yandex.net/v1` - для production использования
 * `http://bunker-api-dot.yandex.net/v1` - для разработки и тестирования

#### version
Type: `string`  
Default: `latest`

Версия нод для выгрузки - `latest` или `stable`.

## Bunker.withContent(node)

Возвращает `true`, если нода имеет контент.

## Bunker.cat(path)

Получает содержимое ноды по пути `path`.

## Bunker.ls(path)

Получает листинг директории по пути `path` как массив нод.

## Bunker.tree(path)

Получает дерево директории по пути `path` как массив нод.

### Нода

Это обычный `plain object`, который вернул нам Бункер в методе `cat`.
