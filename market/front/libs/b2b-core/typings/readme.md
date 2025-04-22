# Settings

В файле settings определяем настройки, которые можно будет переопределить отдельно в каждом проекте (или оставить по умолчанию). Пример такого переопределения - создается файл `b2b-core.d.ts` и заполняется содержимым

```ts
import {ResolverSettings} from '@yandex-market/mandrel/resolver';
import {NoCheckResolverName} from 'app/utils/createSafeResolver/noCheckRemoteResolversNames';

declare module 'b2b-core/shared/utils/createSafeResolver/types' {
    export type NoCheckResolverSettings<P> = ResolverSettings<P> & {
        name: NoCheckResolverName;
    };
}
```
