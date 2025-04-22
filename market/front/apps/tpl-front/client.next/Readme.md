# Как мы пишем клиент

## Slices

Наиболее предпочтительный способ использования redux

- дефолтом экспортируем редьюсер
- экспортируем тип экшенов
- экспортируем экшены
- в случае, когда экшен не меняет стейт слайса, но относится к описываемой в стейте сущности, прописываем экшен в слайсе c обработчиком `identity` из `ramda`

```typescript
// client.next/pages/SomePage/slices/orders.ts

import {identity} from "ramda";
import {createSlice, PayloadAction} from '@reduxjs/toolkit';

const initialState: State = {
    count: 0,
    data: [],
};

const ordersSlice = createSlice({
    name: 'orders',
    initialState,
    reducers: {
        updateOrders: identity,
        updateOrdersFulfilled: (state, {payload}: PayloadAction<{ orders: Order[] }>) => {
            state.count = payload.orders.length;
            state.data = payload.orders;
        },
        updateOrdersFailed: state => {
            state.count = null;
            state.data = null;
        },
    },
});

export type OrdersActions = typeof ordersSlice.actions;

export const {updateOrders, updateOrdersFulfilled, updateOrdersFailed} = ordersSlice.actions;
export default ordersSlice.reducer;
```

```typescript
// client.next/pages/SomePage/actions/index.ts

import type {OrdersActions} from '../slices/orders';

export type Actions = OrdersActions &
// остальные типы экшенов через &
```

## Actions

Для создания экшенов используем `createAction` из `@reduxjs/toolkit`

В коде могут встречаться старые варианты создания экшенов через `typed-actions` или `~/utils/typed-redux`,
такие экшены надо по возможности переводить на `@reduxjs/toolkit`

### Пример создания экшенов через @reduxjs/toolkit с использованием в эпиках

#### Создаем экшены
```typescript
// client.next/pages/SomePage/actions/updateData.ts

import {createAction} from "@reduxjs/toolkit";

import {noPayload} from 'client.next/utils/reduxjs-toolkit/noPayload'

const actions = {
    updateData: createAction('pages/SomePage/UPDATE_DATA', noPayload),
    updateDataFulfilled: createAction(
        'pages/SomePage/UPDATE_FULFILLED',
        data => ({
            payload: {data}
        })
    ),
    updateDataRejected: createAction(
        'pages/SomePage/UPDATE_DATA_REJECTED',
        error => ({
            payload: {error}
        })
    )

export const {updateData, updateDataFulfilled, updateDataRejected} = actions;
export type UpdateDataActions = typeof actions;

// console.log(updateData())
// {type: 'pages/SomePage/UPDATE_DATA', payload: undefined}

// console.log(updateDataFulfilled(someData))
// {type: 'pages/SomePage/UPDATE_FULFILLED', payload: {data: someData}}
 ```

- Тип экшена именуем как `pages/PageName/ACTION_NAME`, например, `pages/SomePageName/UPDATE_ORDER`
- Если экшен без payload, прокидываем вторым аргументом `noPayload` из `client.next/utils/reduxjs-toolkit/noPayload.ts`.
  <details>
    <summary>Зачем нужно это делать</summary>
    <br>
    Если не передавать <code>noPayload</code>, при вызове экшен креатора в payload попадет все, что указано в 1-ом аргументе.
    <br>
    В некоторых случаях это приведет к тому, что payload будет слишком большим и будет замедлять работу приложения
    <br><br>
    Например, если экшен креатор используется как обработчик события, в payload попадет весь event

    ```typescript jsx
    import {createAction} from "@reduxjs/toolkit";

    const openModal = createAction('pages/SomePage/OPEN_MODAL');
    ...
    const dispatchOpenModal = useAction(openModal);

    <button onClick={dispatchOpenModal}>Open beautiful modal</button>

    // клик по кнопке приведет к диспатчу экшена
    {
      type: 'pages/SomePage/OPEN_MODAL',
      payload: {
        target: { /*...*/ },
        currentTarget: { /*...*/ },
        /*
        и прочие поля SyntheticEvent
            |\__/,|   (`\
          _.|o o  |_   ) )
        -(((---(((--------
       */
      }
   }
   ```
  </details>
- Если экшен с payload, прокидываем вторым аргументом маппер аргументов креатора в payload
  (обязательно типизируем аргумент маппера для типизации создаваемых экшенов!)
  <br>
  https://redux-toolkit.js.org/api/createAction#using-prepare-callbacks-to-customize-action-contents
- Создаем экшен креаторы внутри объекта, чтобы было проще экспортить тип экшенов

#### Экспортим экшены и их типы в индексном файле

```typescript
// client.next/pages/SomePage/actions/index.ts

import type {UpdateDataActions} from './updateData';
// импортим остальные типы экшенов

export * from './updateData';
// экспортим остальные экшены

export type Actions = UpdateDataActions &
// остальные типы экшенов через &
```

## Reducers

- для создания редьюсеров используем `createReducer` из `@reduxjs/toolkit`
- для матчинга экшенов используем `builder` для лучшей типизации (если использовать "Map Object", тип экшена будет `any`)

```typescript
// client.next/pages/SomePage/reducers/orders.ts
import {createReducer} from '@reduxjs/toolkit';

import {STATUS, Status} from '~/types/data';

import type {PageState} from 'shared/pages/PageName';

import {
    fetchOrders,
    fetchOrdersFulfilled,
} from '../actions';

/*
type PageState = {
    orders: {
        data: Order[];
        status: Status;
    }
    ...
}
 */
type State = PageState['orders'];

export default createReducer<State>(
    {
        data: [],
        status: STATUS.done,
    },
    builder =>
        builder
            // 1ый аргумент addCase ожидает тип экшена,
            // но если в экшен креаторе .toString() возвращает тип (как в случае креаторов, созданных через createAction из @reduxjs/toolkit)
            // можно использовать сам экшен креатор
            .addCase(fetchOrders, state => {
                state.status = STATUS.pending;
            })
            .addCase(fetchOrdersFulfilled, (state, action) => {
                state.data = action.payload.orders;
                state.status = STATUS.done;
            })
);
```

## Epics

- Для фильтрации экшенов в эпиках нужно обязательно использовать `filter(actionCreator.match)` (в случае фильтрации по нескольким экшенам `filter(isAnyOf(actionCreator1.match, actionCreator2.match))`).
  <br>Раннее использовавшиеся `action$.ofType(actionCreator.type)` и `ofType(actionCreator.type)` не приводят к достаточной типизации.
- для типа эпиков используем тип `Epic`, который принимает первым аргументом `State`, вторым экшны (по умолчанию достаточно использовать `type Actions` из экшнов)

```typescript
// client.next/pages/SomePage/epics/data.ts

import {isAnyOf} from "@reduxjs/toolkit";

import type {Epic} from '~/types/redux';

import {
    Actions,
    updateData,
    updateDataFulfilled,
    updateDataRejected,
} from '../actions';
import type {State} from '../reducers';

export const updateDataEpic: Epic<State, Actions> = (action$, state) =>
    action$.pipe(
        filter(updateData.match),
        // теперь экшен будет типа UDATE_DATA
        // ...
    )

export const updateDataCompletedEpic: Epic<State, Actions> = (action$, state) =>
    action$.pipe(
        filter(isAnyOf(updateDataFulfilled.match, updateDataRejected.match)),
        // теперь экшен будет либо типа UPDATE_DATA_FULFILLED, либо типа UPDATE_DATA_REJECTED
        // ...
    )
```
