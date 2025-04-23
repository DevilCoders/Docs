# `@duffman-int/service-furita`

Пакет `@duffman-int/service-furita` для работы с Furita API.


## Использование

Модуль экспортирует сервис, модели и типы к моделям.

```typescript
import * as furita from '@duffman-int/service-furita';

export const services = {
    [furita.id]: furita.service;
};

export const models = prepareModels({
    'get-rules': furita.models.get_rules_v1,
});
```

типы моделей можно получить так:
```typescript
import type { models } from '@duffman-int/service-furita';

async function f(core: Core) {
    const params: models.GetRulesV1.Params = {};
    const result = await core.request('get-rules', params);
}
```

## Конфигурация

```typescript
import { id as furitaId } from '@duffman-int/service-furita';

class Core extends DuffmanCore<...> {
    // ...
    static config = {
        services: {
            [furita]: {
                defaultOptions: {}
            }
        }
    }
    // ...
}
```
