# Резолверы

### Документация
- [mandrel](https://github.yandex-team.ru/market/mandrel/tree/master/src/resolvers)
- [wiki](https://wiki.yandex-team.ru/market/frontend/apiary/#rezolvery)
- [createSafeResolver](../utils/createSafeResolver/README.md)

shared/resolvers/getSuppliersFullInfo.js:
```js
const {unsafeResource} = require('@yandex-market/mandrel/resolver');
const {createResolver} = require('shared/utils/createSafeResolver');

export const getSuppliersFullInfo = createResolver(
    (ctx, params = {}) => unsafeResource(ctx, 'mbiPartner.getSuppliersFullInfo', params),
    {name: 'getSuppliersFullInfo', remote: true},
);
```
Использование на клиенте:
```js
import {from} from 'rxjs';
import {mergeMap} from 'rxjs/operators';
import {ofType} from 'redux-observable';
import context from '@yandex-market/mandrel/clientContext';
import {getSuppliersFullInfo} from 'shared/resolvers/getSuppliersFullInfo';

export const RemoteResolverEpicExample: Epic<State, Actions> = action$ => action$
    .pipe(
        ofType(SOME_ACTION),
        mergeMap(() => from(getSuppliersFullInfo(context))),
    );
```

Использование на сервере:
```js
// <app/stout/pages/html/HtmlSomeSuperPage/index.js>
import {createContext} from '@yandex-market/mandrel/context'; // Серверная фабрика создания контекста

function HtmlSomeSuperPage() {
    const initialState = getInitialState(createContext(this));

    this.push(promiseToResponse(this.buildInitialState(initialState)), 'initialState');
}

// <app/stout/pages/html/HtmlSomeSuperPage/getInitialState.js>

import {getSuppliersFullInfo} from 'shared/resolvers/getSuppliersFullInfo';

export const getInitialState = (ctx) => getSuppliersFullInfo(ctx);
```
