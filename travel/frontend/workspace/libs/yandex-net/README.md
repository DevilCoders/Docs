# yandex-net

Платформо-независимые утилиты для интеграции сервисов с инфраструктурой Яндекса.
Объединяет разрозненные реализации в единый набор инструментов.
Требование - поддержка Web API (URL / URLSearchParams / Fetch API)

## Структура

-   [core](./core) - основная логика и утилиты, реализованы без какой-либо привязки к инструментам
    -   [tvm](./core/tvm) - утилиты по получению исходящих и верификации входящих тикетов
    -   [blackbox](./core/blackbox)
    -   [uatraits](./core/uatraits) - запрос для детекции устройства
    -   [yandexuid](./core/yandexuid) - утилиты для работы с yandexuid
-   [express](./express) - Пример миддлвар для экспресса поверх ядра

## Uatraits

Внешний сервис для комплексной детекции устройства пользователя.

-   [Сборная информация](https://wiki.yandex-team.ru/analytics/search/m/tech/library/uatraits)
-   [Список полей](https://wiki.yandex-team.ru/Morda/browserDetect)

### Использование

Клиент

```typescript
import { UatraitsClient } from 'yandex-net/core/uatraits';

const client = new UatraitsClient({ url: 'https://...' });
// ...
```

## Blackbox

[Основная документация](https://docs.yandex-team.ru/blackbox/)

## Ядро

### TVM

Используется для верификации межсервисных запросов.
Референсы:

-   `@yandex-int/express-tvm` - основной источник, реализует получение tvm-тикетов
-   [https://wiki.yandex-team.ru/passport/tvm2](https://wiki.yandex-team.ru/passport/tvm2)
-   [https://wiki.yandex-team.ru/passport/tvm2/stbrief](https://wiki.yandex-team.ru/passport/tvm2/stbrief)

Реализовано:

-   Получение тикетов зависимых сервисов в понятном формате и с гарантией наличия всех тикетов
-   Проверка пришедшего тикета

Получение тикетов

```typescript
import { getTvmTickets } from 'yandex-net/core';
// ...
const tickets = await getTvmTickets({
    url: 'http://localhost:9911',
    token: '1122334587238646t273647263',
    dependencies: ['blackbox', 'serviceFoo', 'serviceBar'],
});
// { blackbox: { id: 123, name: 'blackbox', ticket: '123:x..' }, serviceFoo: { id: 234, ... }, serviceBar: { id: 234, ... } }
console.log(tickets);
```

Авторизация входящих запросов

```typescript
import {
    validateIncomingTvmTicket,
    checkTvmAuthPolicy,
    YandexHeaderName,
    TvmAuthPolicy,
} from 'yandex-net/core';
// ...
async function myHandler(req, res) {
    const incomingTicket = await validateIncomingTvmTicket(
        {
            url: 'http://localhost:9911',
            token: '1122334587238646t273647263',
        },
        req[YandexHeaderName.X_YA_SERVICE_TICKET],
    );
    const auth = checkTvmAuthPolicy(TvmAuthPolicy.OPTIONAL, [123, 234], incomingTicket);

    if (!auth.authorized) {
        console.warn(auth.message);
    }
}
```

### NextJS

Утилиты для API-роутов и миддлвар

#### Middleware

```typescript
import { setNextMiddlewareYandexUid } from 'yandex-net/next/middleware';
import { NextRequest, NextResponse } from 'next/server';

export async function middleware(req: NextRequest) {
    const res = NextResponse.next();

    setNextMiddlewareYandexUid(req, res);
    return res;
}
```

#### Api routes

```typescript
import { proxyApiRequest } from 'yandex-net/next/api-routes';
import { getTvmOutgoingTickets, getUatraits } from 'yandex-net/core';
import { NextApiRequest, NextApiResponse } from 'next';

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
    const tvm = await getTvmOutgoingTickets({
        url: '...',
        token: '...',
    });
    const uatraits = await getUatraits({
        url: '...',
    });

    return proxyApiRequest({
        url: 'http://foo',
    });
}
```

### Express

Миддлвары экспресса поверх утилит ядра

```typescript
import {
    expressTvmMiddleware,
    expressUatraitsMiddleware,
    expressYandexUidMiddleware,
} from 'yandex-net/express';
// ...
// Добавляем токены в req.tvm
app.use(
    expressTvmMiddleware({
        url: '...',
        token: '...',
    }),
);
// Детектим устройство, кладем в req.uatraits
app.use(
    expressUatraitsMiddleware({
        url: '...',
    }),
);
// Если позволяют условия - ставим yandexuid
app.use(expressYandexUidMiddleware());
```

### Описание

TODO

#### Использование

TODO
