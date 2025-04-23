# Сервисы и модели
Примеры сервисов и моделей есть в этой папке.

## Использование
В приложении
```ts
import { prepareModels } from '@duffman-int/core';
import * as tvm from '@duffman-int/service-tvm';

export const tvmTickets = Symbol('tvm:tickets');

const models = prepareModels({
  [tvmTickets]: tvm.models['tickets/v1'],
  checkUser: tvm.models['check-user/v1']
});

const services = {
  [tvm.id]: tvm.service
};

export { models, services };
```

## Сборка

Собрать всё:
```sh
make
```
Собрать и следить:
```sh
make watch
```

Отдельный сервис:
```sh
cd service-akita
# собрать
make
# или собрать и следить
make watch
```

## Версионирование и публикация пакета
Схема версионирования:
  * **patch** — фиксы и неломающие изменения (в том числе добавление новых атрибутов в ответы моделей);
  * **minor** — новые модели;
  * **major** — ломающие изменения.

Публикация (не забыть обновить версию перед публикацией):
```sh
cd service-akita
make publish
```

## Структура пакета
  * `service/index.ts` — сервис (в виде `Core.Service<...>`).
  * `service/default-config.ts` — конфиг (в формате описаном в Duffman `lib/core/service-config.ts`);
  * `models/...` — модели (в виде `Core.Model<...>`);
  * `index.ts` — входная точка;

### Сервис
[пример](./service-tvm/service/index.ts)

Экспортирует дефолтную функцию с сигнатурой `Core.Service<...>`.

В 99% случаев должен иметь свойство `service[flags.defaultConfig]` с функцией возвращающей дефолтный конфиг. Обычно это функция которая лежит в `default-config.ts`.


### Входная точка (`index.ts`)
[пример](./service-tvm/index.ts)

Экспортирует:
  * `id` — идентификатор сервиса;
  * `service` — сервис;
  * `models` — объект с моделями.

Примерно так:
```ts
import service, { id } from './service';
import models from './models';

export { id, service, models };
```
Если моделей мало, то можно их импортировать прямо тут
```ts
import service, { id } from './service';
import myModel from './models/my-model';
const models = { myModel } as const;

export { id, service, models };
```

### Модель
[пример](./service-tvm/models/check-user/v1/index.ts)

Экспортирует класс унаследованный от `duffman.Model`.
