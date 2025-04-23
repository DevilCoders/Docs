# maps-proto-schemas

В пакете собранны схемы ответов карточных бекендов в protobuf формате.
Все схемы выкачиваются из [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/).

legacy-версия, которая выкачивала пробафы из аркадии через SVN: https://github.yandex-team.ru/maps-legacy/maps-proto-schemas

## Использование

1) Установка:
```
npm install @yandex-int/maps-proto-schemas --save-prod --save-exact
```

2) Подключение и использование:
```js
const protobuf = require('protobufjs');
const schemas = require('@yandex-int/maps-proto-schemas').get();

// Переменная schemaPath должна содержать имя схемы, начиная с yandex.maps.proto.
protobuf.loadSync(schemas).lookup(schemaPath);
```

Существуют возможность получить только избранные схемы.
Для этого необходимо передать массив интересующих поддиректорий в функцию `get`. Пример:

```js
const schemas = require('@yandex-int/maps-proto-schemas').get(['atom', 'common2']);
```

Подключение объявлений типов TypeScript:

```ts
import {yandex} from '@yandex-int/maps-proto-schemas/types';

//example:
let Response: yandex.maps.proto.common2.Response;
```

## Contributing

Если вы просто хотите выпустить новую версию пакета для конкретной ревизии аркадии — просто создайте PR с новой версией в `package.json`. CI соберет и выложит все самостоятельно.

### Установка зависимостей

```sh
make install
```

### Новая версия пакета

Версионирование идет по ревизиям Аркадии. Чтобы применить сменить версию на текущую ревизию:

```sh
make version
```

Если нужна версия пакета для любой прошлой ревизии, укажите требуемую ревизию в `package.json` `version` и запустите сборку.

### Сборка

Чтобы локально пересобрать текущую версию схем, выполните:

```sh
make
```

### Публикация

Публикация происходит автоматически при мердже в транк, если версия в `package.json` изменилась.
