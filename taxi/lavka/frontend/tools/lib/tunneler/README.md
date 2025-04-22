## Полезные ссылки

- [Документация](https://doc.yandex-team.ru/si-infra/tunneler/)

## Пример локального использования

```ts
import {openTunnel} from '@lavka/tools/lib/tunneler'

const tunneler = await openTunnel({
    localport: 3000,
    domains: ['yandex-team.ru'],
    version: 1,
})

await tunneler.close()
```

## Пример использования в CI

```ts
import {openTunnel} from '@lavka/tools/lib/tunneler'

const tunneler = await openTunnel({
    localport: 3000,
    user: config.robot,
    hosts: ['tun.si.yandex-team.ru'],
    version: 2,
    cloud: 'yp',
})

await tunneler.close()
```
