# openapi

## Roadmap

> Пакет находится в разработке, **на данный момент отсутствует**:

-   [ ] CLI
-   [ ] Public API с реэкспортами типов и сгенерированных клиентов
-   [ ] Функционал сборки openapi схем из proto файлов (обертка над ya make)
-   [ ] Дедупликация и типов из разных схем (самое очевидное - ProtobufAny)
-   [ ] Генерация прокси для создания автоматизированных BFF-прослоек
-   [ ] Генерация контрактов для корректной обработки ошибок и неожиданного поведения
-   [ ] Генерация BFF болиерплейта
-   [ ] Генерация DI (специфика Yandex Travel)
-   [ ] Точечная генерация редакс болиерплейта (сейчас только базовая обертка под эндпоинт)

## Установка

```shell
yarn add -D openapi
```

## Использование

Можете посмотреть [Примеры использования](./examples)

### Создайте и опишите .openapi.config.js

```javascript
/**
 * @type {import('openapi').UserConfiguration}
 */
module.exports = {
    // Директория для сгенерированных клиентов
    outputRoot: 'shared/api/gen',
    // Путь к папке со схемами
    sourceRoot: 'my-swagger-folder',
    // Директория для сгенерированных утилит и тонкого болиерплейта
    helpersRoot: 'shared/api',
    // Список swagger/openapi файлов
    include: ['first.yaml', 'foo/bar/baz.yaml', 'openapi.json'],
    generate: [
        // апи-клиент
        'api',
        // редаксовские фабрики
        'redux',
        // эффекты
        'effector',
    ],
    output: {
        // shared/api/gen/<service>/common/shared-types.ts
        sharedTypes: 'common/shared-types.ts',
        // shared/api/gen/<service>/common/endpoint-types.ts
        endpointsTypes: 'common/endpoint-types.ts',
        // shared/api/gen/<service>/api.ts
        api: 'api.ts',
        // shared/api/gen/<service>/redux.ts
        redux: 'redux.ts',
    },
};
```

### Добавьте скрипт запуска в package.json

> В разработке

```json
{
    "scripts": {
        "api-make": "openapi make",
        "api-build": "openapi generate"
    }
}
```

```shell
yarn api-build
```

### Использование сгенерированных клиентов

#### API

Сгенерированный апи клиент является классом с методами, привязанными к эндпоинтам.
Вся настройка сведена к HTTP-клиенту, передающемуся в качестве зависимости в конструктор.

> Базовые HTTP-клиенты в разработке

```typescript
// где-то в проекте
import { MyServiceApi } from '@/shared/api/generated/my-service/api';
import { BaseFetchHttpClient } from '@/shared/api/helpers/builtin/base-http-client';

const myServiceApi = new MyServiceApi({
    httpClient: new BaseFetchHttpClient({
        baseUrl: 'https://my-api.org',
    }),
});

/**
 * POST https://my-api.org/super-entity?authorUserId=my-id-123
 * BODY { "title": "foo", "content": "bar" }
 */
myServiceApi.createNewSuperEntity({
    authorUserId: 'my-id-123',
    body: {
        title: 'foo',
        content: 'bar',
    },
});
```

#### Effector

Для эффектора генерируются атомарные эффекты под каждый эндпоинт, домен под сервис и общий эффект запроса.
Настройка сводится к переопределению базового эффекта.

```typescript
// shared/api/helpers/effector-request-fx.ts (Этот файл является редактируемым)
import { BaseFetchHttpClient } from '@/shared/api/helpers/builtin/base-http-client';
// ..................
const client = new BaseFetchHttpClient({
    baseUrl: 'https://my-api.org',
});
requestFx.use(options => client.request(options));
```

```typescript
// где-то в проекте
import {
    createNewSuperEntityFx,
    getUserAccountFx,
} from '@/shared/api/generated/my-service/effector';

/**
 * POST https://my-api.org/super-entity?authorUserId=my-id-123
 * BODY { "title": "foo", "content": "bar" }
 */
createNewSuperEntityFx({
    authorUserId: 'my-id-123',
    body: {
        title: 'foo',
        content: 'bar',
    },
});

/**
 * GET https://my-api.org/users/accounts/my-id-123
 */
getUserAccountFx({
    id: 'my-id-123',
});
```

## Рецепты

### NX

Для корректной работы с nx вам требуется описать конфигурацию скриптов

> In progress

```json
{
    "nx": {
        "namedInputs": {
            "openapi-proto": [
                {
                    "env": "TODO_ADD_YA_MAKE_TOKEN_NAME"
                },
                "{workspaceRoot}/../../../spec/api/my-folder/**/*.proto"
            ],
            "openapi": ["{projectRoot}/specs/**/*.json"]
        },
        "targets": {
            "api-make": {
                "inputs": ["openapi-proto"],
                "outputs": ["specs/**/*.json"],
                "dependsOn": ["api-make"]
            },
            "api-build": {
                "inputs": ["openapi"],
                "outputs": ["shared/api/generated"],
                "dependsOn": ["^api-make", "api-build"]
            }
        }
    }
}
```
