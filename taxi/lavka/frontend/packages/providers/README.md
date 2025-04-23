# Providers

## Структура

Пакет разделен на три слоя:

- `clients/*/api.ts` - транспортный слой(необязательный), в модуль передаем уже обработанные данные для запроса. Модуль ходит в нужную ручку с нужными параметрами запроса. Слой не содержит бизнесовой или какой-либо умной логики.

- `clients/*/context-client.ts` - слой с бизнес-логикой. Все умные действия происходят здесь.

- `bff-adapters` - транспортный слой, но с интерфейсом, повторяющим слой `clients`. Вместо выполнения действия на клиенте, `bff-adapters` ходит на `bff`, а уже там вызывается нужный метод из `clients`.

Практически все функции в `api`, `context-client` содержать постоянный первый аргумент - `ctx: Context`, содержащий контекст исполнения функции. Эти функции являются внутренними и нужны для корректной работы на сервере (нужно завязаться на `request`)

### Пример реализации

Для простых случаев можно не создавать отдельный api слой

```ts
// context-client.ts

export function retrieve(ctx: Context, body: Request) {
  return ctx.getConfig().requestFn<Request, Response>({
    method: 'POST',
    url: '/lavka/v1/cart/v1/retrieve',
    body,
  })
}
```

Можно разделить api и context-client. Это имеет смысл, если

- В клиенте много логики, можно немного разгрузить
- Одна ручка может использоваться несколько раз внутри клиента

```ts
// api.ts

export function retrieve(ctx: ExternalContext, body: Request) {
  return ctx.requestFn<Request, Response>({
    method: 'POST',
    url: '/lavka/v1/cart/v1/retrieve',
    body,
  })
}

// context-client.ts

export async function retrieve(ctx: Context, body: Request) {
  const res = await api.retrieve(ctx.getConfig(), body)

  return res
}
```

#### Клиент

Экспортируемые функции фиксирует в качестве своего контекста глобальный контекст.

```ts
// api.ts

import * as contextApi from './context-api'

const ctx: Context = { ... }

export const retrieve = bindCtx(ctx, contextApi.retrieve)
```

#### Сервер

Для серверной части существует отдельная функция, создающая объект со всеми экспортируемыми функциями и привязывающая к ним свой внутренний контекст.

```ts
// api.ts

export function initializeCtxApi(config) {
  const ctx: Context = { ... }

  return {
    retrieve: bindCtx(ctx, contextApi.retrieve),
  }
}
```

## Использование

### Клиент

```ts
import {cartClient} from '@lavka/providers'

cartClient.initializeClient({ ... })

cartClient.retrieve({
  cart_id,
  position: { location },
})
```

### Сервер

```ts
import {cartClient} from '@lavka/providers'

const cartClientInst = cartClient.initializeCtxClient({ ... })

cartClientInst.retrieve({
  cart_id,
  position: { location },
})
```

Для серверной части есть одна функция, инициализирующая все клиенты в провайдерах. Теоретически ее можно использовать на клиенте, но не рекомендуется, т.к. тянет за собой весь код пакета.

```ts
import {providersClient} from '@lavka/providers'

const providers = providersClient.initializeCtxClient({
  common: { requestFn }
  cart: { ... }
})

await providers.cart.retrieve({
  cart_id,
  position: { location },
})
```
