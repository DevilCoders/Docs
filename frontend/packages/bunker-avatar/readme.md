# bunker-avatar

Парсер ссылок на Аватариницу из mime ноды Бункера. Испольуется в [bunker-to-js](https://github.yandex-team.ru/project-stub/bunker-to-js).

Матчится на все ноды с mime-типом `image/svg+xml` и присутствующим `avatar-href` в mime.

## Usage

```js
var bunker = require('bunker-to-js');
bunker().parse(require('bunker-avatar'));
```

## API

### bunker-avatar

Функция парсер, которая запишет в `node.content` результат парсинга `avatar-href` в mime.
Убирает протокол из URL — 'http://avatarnica.ru/image/bla.png' будет переведено в '//avatarnica.ru/image/bla.png'.

### bunker-avatar.withProtocol

Тоже самое, только оставляет протокол в покое.
