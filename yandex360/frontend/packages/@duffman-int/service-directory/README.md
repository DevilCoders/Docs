# `@duffman-int/service-directory`

Пакет `@duffman-int/service-directory` для работы с Directory API.

https://api-internal.directory.ws.yandex.net/docs/playground.html

## Использование
Модуль экспортирует сервис, модели и типы к моделям.

```typescript
import * as directory from '@duffman-int/service-directory';

export const services = {
    [directory.id]: directory.service;
};

export const models = prepareModels({
    'get-department': directory.models.get_department_v1,
});
```

типы моделей можно получить так:
```typescript
import type { models } from '@duffman-int/service-directory';

async function f(core: Core) {
    const params: models.GetDepartmentV1.Params = { directoryId: 42 };
    const result = await core.request('get-department', params);
}
```

## Конфигурация
Из-за особенности API директории у сервиса есть специальная настройка `addUidHeader` выставление
которой добавляет в запросы заголовок `x-uid: <UID>` с uid-ом текущего пользователя. В зависимости
от вашего TVM-сервиса это заголовок может быть ненужен (и даже вреден). Что бы его выключить,
нужно добавить конфиг в ядро.

```typescript
import { id as directoryId } from '@duffman-int/service-directory';

class Core extends DuffmanCore<...> {
    // ...
    static config = {
        services: {
            [directoryId]: {
                defaultOptions: {
                    addUidHeader: false
                }
            }
        }
    }
    // ...
}
```
