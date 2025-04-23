# Резолверы

Резолверы -- функции для получения определённых сущностей (чаще всего инкапсулируют в себе работу с одним или более `Resource`'ами, но это не является обязательным условием), могут выполнять какую-либо предобработку параметров или постобработку полученных данных и возвращают `Promise`.

Должны быть сгруппированы по сущностям, с которыми они работают.

Резолверы представляются в виде функции, которые первым аргументом принимают `Context` (`import type {Context} from '@yandex-market/mandrel/Context'`). Вторым аргументом может идти параметр резолвера, если он его принимает.

Такой порядок аргументов и каррирование необходимо для удобного использования резолвера в цепочках и композициях.

Для создания резолверов используются `createResolver` и `createBulkResolver`.

Пример:
```js
import type {Context} from '@yandex-market/mandrel/context';
import {getCookie, getHeader, getParam} from '@yandex-market/mandrel/context';
import {createResolver, unsafeResource} from '@yandex-market/mandrel/resolver';

export const resolveFooBar = createResolver(async (ctx: Context, options: Options): Promise<?FooBar> {
    const kek = getParam(ctx, 'kek');
    const lol = getCookie(ctx, 'lol');
    const bar = getHeader(ctx, 'X-Bar');

    if (kek == null || lol == null || bar == null) {
        return null;
    }

    const {foo} = options;

    return await unsafeResource(ctx, 'some.method', {kek, lol, foo, bar});
}, {
    cache: {
        level: 'request',
    },
    remote: true,   // разрешаем вызывать с клиента
});
```

При вызове удалённых (`remote`) резолверов с клиента, контекст импортируется из модуля `clientContext`.
Удаленные резолверы не работают, если их импортировать через реэкспорт. Пример:
```js
// ...resolvers/staff/resolveStaffByUsername.js

export const resolveStaffByUsername = createResolver(
    (ctx: Context, params: ResolveStaffItemParams): Promise<Result> => fetchStaffItem(ctx, params),
    {
        remote: true,   // разрешаем вызывать с клиента
        name: 'resolveStaffByUsername',
    }
);

// ...resolvers/staff/index.js

export {resolveStaffByUsername} from './resolveStaffByUsername';

// ...epics.js

/*
 * Неправильный импорт резолвера, на клиенте выкинет ошибку:
 * Error: Resolver "resolveStaffByUsername" is non-remote
 */
import {resolveStaffByUsername} from '.../staff';

/*
 * Правильный импорт резолвера
 */
import {resolveStaffByUsername} from '.../staff/resolveStaffByUsername';

const loadMoreColleaguesEpic: WidgetEpic<Actions, Data, {}> = (actions$, facade) =>
    actions$.pipe(
        ofType(LOAD_STAFF),
        mergeMap(() => {
            return fromResolver(resolveStaffByUsername, {...}).pipe(...);
        }),
        catchError(() => EMPTY)
    );
```

# Соглашения
- Имена имеют префикс `resolve`.
- Имена синхронных резолверов имеют суффикс `Sync`.
- Для вызова ресурсов используется функция `unsafeResource`.
- Для создания резолверов используется функция `createResolver`, а для синхронных резолверов -- `createSyncResolver`.
- Для получения stout page/request используются функции `getStoutPage` и `getStoutRequest` из `context`.
- Использовать `getStoutPage` и `getStoutRequest` стоит только в том случае, если по-другому получить данные нельзя.
