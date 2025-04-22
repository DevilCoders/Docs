# Duffman TS

## Сервисы и модели

### Использование

```ts
import akita, { auth, other } from '@duffman-int/service-akita';
/**
  * akita.service — сервис
  * akita.resolveModel — получить собственно модель по дескриптору
  * auth, other — дескриптор модели (Symbol)
  */

export const services = {
    akita: akita.service
} as const;

export const models = {
    [auth]: akita.resolveModel(auth), // «приватная» модель
    'other': akita.resolveModel(other), // обычная модель
} as const;
```

«Приватную» модель можно вызвать только зная её символ, это защита от вызова
таких моделей из балковых ручек (`/web-api/models/v1` и т.п.)
Таким образом где-то в middleware auth мы можем написать
```ts
import { auth } from '@duffman-int/service-akita';

export default async (req, res, next) => {
    const core = req.core;
    core.auth.set(await core.request.safe(auth));
    next();
}
```

## Core

### Core#request

### Core#service

### Core#auth

### Core#got
Пока очень *generic*
```ts
type coreGot = (url: string, options: any) => Promise<any>;
```

