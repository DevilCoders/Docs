# Как добавить новую страницу?

Пример: https://github.yandex-team.ru/Metrika/frontend/pull/2052/files

### Создать путь для новой страницы
services/metrika/client/constants/routes.ts
```typescript
export const EXAMPLE_URL = '/example';
```

### Разрешить его внутри nginx
services/metrika/nginx/conf.d/default.conf.template
```
location /example {
  include incl.d/timeouts-default.conf;
  include incl.d/proxy/metrika.conf;
}
```
### Добавить в appRouter, установив подходящую middleware

services/metrika/server/router/app.ts
```typescript
// новая страница
appRouter.get(EXAMPLE_URL, middleware, index);
```

### Создать корневой шаблон

services/metrika/client/pages/__Example/index.tsx__

Название папки зависит от адаптивности страницы: ExampleDesktop, ExampleTouch

Когда поддерживается сразу desktop + touch, то постфикс можно не ставить — Example

```typescript
import React, { FC } from 'react';

export const ExamplePage: FC = () => {
    return (
        <div>Example</div>
    );
};
```

### Создать заглушки для инициализации

services/metrika/shared/routes/init/__example/client.ts__
```typescript
import { Store } from 'redux';

// eslint-disable-next-line @typescript-eslint/no-unused-vars
export const goalsInit = async (store: Store) => {
    // fetch data
};
```

services/metrika/shared/routes/init/__example/server.ts__
```typescript
import { Store } from 'redux';
import { defaultInit } from '../default/server';
import { initedDuck } from '@metrika/shared/ducks/inited';
import { Request } from 'express';
import { isAuthenticated } from '@metrika/server/auth/utils';

export const exampleInit = async (store: Store, req: Request) => {
    if (!isAuthenticated(req)) {
        return;
    }

    await defaultInit(store, req);

    store.dispatch(initedDuck.actions.init());
};
```


### Добавить страничку в маршрутизаторы

services/metrika/shared/routes/client.ts
```typescript
= {
    id: 'example',
    path: EXAMPLE_URL,
    render: renderPageRoute(ExamplePage, {}),
    init: exampleInit,
    storeConfigurator: configureStore,
    transfer,
}
```

services/metrika/shared/routes/server.ts
```typescript
= {
    id: 'example',
    path: EXAMPLE_URL,
    init: exampleInit,
    storeConfigurator: configureStore,
}
```

