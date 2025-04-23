# Ресурсы

В пакете в формате [descript](https://github.com/pasaran/descript3)-деклараций описаны две ручки Яндекс.Директа:
- `/meta/<page-id>` - https://wiki.yandex-team.ru/users/larichevmn/s2s/
- `/widget_settings` - https://wiki.yandex-team.ru/users/disaev/s2s-dlja-nativnyx-blokov/vidzhetov/

Параметры блоков также описаны в `index.d.ts` пакета

Для их использования надо передавать в метод дескрипт-конфиг базового блока с заданными протоколом, хостом, портом. Далее можно расширять необходимыми параметрами,
добавлять маппинги.

## Пример использования:

```typescript

import { getYandexDirectMeta } from '@vertis/ads';
import de from 'descript';

const yandexDirectBaseConfig = de.http<RequestContext, {}, unknown>({
    block: {
        protocol: process.env.DIRECT_PROTOCOL + ':',
        port: Number(process.env.DIRECT_PORT) || 80,
        hostname: process.env.DIRECT_HOSTNAME,
        family: 6,
    },
    options: {
        logger: DescriptLogger,
        name: 'direct',
    },
});


const request = getYandexDirectMeta(yandexDirectBaseConfig)({
    options: {
        params: ({ context, params }: { context: RequestContext; params: RequestParams }) => {
            return {
                url: context.req.context.fullUrl || '',
                referer: context.req.headers.referer || '',
                pageId: params.pageId,
                clientIp: context.req.context.clientIp || '',
                headers: context.req.headers,
            };
        },
        before: guard(({ context }) => !context.req.context.isRobot),
        after: ({ result }) => result.result,
        name: 'direct:GET /meta/{page-id}',
    },
});
```
