# Как мы пишем клиент

## Actions

- экшны именуем как `NAME_SPACE/ANOTHER_NAMESPACE/ACTION`, например, `PAGE/STAT_ORDERS/UPDATE` или `I18N/INIT`
- внутри файла переменную с типом экшна называем по самому названию действия, **без неймспейса**, например `UPDATE`, и
  экспортируем ее
- для создания экшнов креаторов используем `createActions`
- при этом экшн креатор описывается следующим образом:
    - если у нас есть `payload`: `(arg: Type, arg2: Type2, ...) => action(<payload data>)`
    - если у нас есть еще и `meta`: `(arg: Type, arg2: Type2, ...) => action(<payload data>, <meta>)`
    - если же пэйлоад не нужен, то используется функция `empty`
- экспортируем общий тип для всех экшнов
- созданные экшны **иммутабельные** в глубину

```js
import {createActions, action, empty} from 'typed-actions';

export const UPDATE = 'PAGE/STAT_ORDERS/UPDATE';
export const UPDATE_FULFILLED = 'PAGE/STAT_ORDERS/UPDATE_FULFILLED';
export const UPDATE_FAILED = 'PAGE/STAT_ORDERS/UPDATE_FAILED';

let actions;

export const {
    [UPDATE]: update,
    [UPDATE_FULFILLED]: updateFulfilled,
    [UPDATE_FAILED]: updateFailed,
} = actions = createActions({
    [UPDATE]: empty, // => {type: UPDATE}
    [UPDATE_FULFILLED]: (x: string[]) => action(x), //  => {type: UPDATE_FULFILLED, payload: x}
    [UPDATE_FAILED]: (x: string) => action(x, {sync: true}), // => {type: UPDATE_FAILED, payload: x, meta: {sync: true}}
});

export
type
Actions = typeof actions;
```

## Reducers

- для определения типа стейта используем тип `StateType`, таким образом стейт будет **иммутабельный** (причем в глубину)
  и **строгий**
- для определения типа редьюсеров используем тип `Handlers`, который первым аргументом получает стейт, вторым аргументом
  тип экшнов, и он выведет типы для каждого кэшна и стейта в функция **самостоятельно**
- для создания редьюсеров используем функцию `handleActions`

```js
import {handleActions, type Handlers, type Frozen} from 'typed-actions';
import {STATUS, type Status} from '~/types/data';

import {
    type Actions,
    UPDATE,
    UPDATE_FULFILLED,
    UPDATE_FAILED,
} from './actions';
import type {PageData} from './types';

export
type
State = Frozen < {
    data: PageData,
    status: Status,
} >;

export default handleActions(({
    [UPDATE]: state => ({
        ...state,
        status: STATUS.pending,
    }),

    [UPDATE_FULFILLED]: (state, {payload}) => ({
        ...state,
        data: payload,
        status: STATUS.done,
    }),

    [UPDATE_FAILED]: state => ({
        ...state,
        status: STATUS.failed,
    }),
}: Handlers<State, Actions>));
```

## Epics

- для типа эпиков используем тип `Epic`, который принимает первым аргументом `State`, вторым экшны (по умолчанию
  достаточно использовать `type Actions` из экшнов)
- типы для экшнов будут выведены **автоматически**

```js
import {map} from 'rxjs/operators';
import {ofType} from 'redux-observable';
import type {Epic} from 'shared/types/redux';

import {
    type Actions,
    UPDATE,
    updateDone,
} from './actions';

import type {State} from './';

export const updateEpic
    : Epic<State, Actions>
    = action$ => action$
        .pipe(
            ofType(UPDATE),
            map(() => updateDone()),
        );
```
