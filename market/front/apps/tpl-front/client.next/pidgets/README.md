# Pidgets

Partner Interface Widgets

<img src="https://media.github.yandex-team.ru/user/5825/files/f7ccd580-84dc-11eb-9004-33358b9ccff6" alt="pidgey" style="display: block; margin: auto; max-width: 300px;">

**Содержание**
- [Pidgets](#pidgets)
  - [Принципы работы](#принципы-работы)
  - [Файловая структура](#файловая-структура)
    - [Экшены виджета](#экшены-виджета)
    - [Объявление виджета](#объявление-виджета)
    - [State виджета](#state-виджета)
    - [Редюсер виджета](#редюсер-виджета)
    - [View и вложенные компоненты](#view-и-вложенные-компоненты)
    - [Epics виджета](#epics-виджета)
      - [Работа с данными до маунта виджета](#работа-с-данными-до-маунта-виджета)
      - [Работа с данными в момент маунта виджета](#работа-с-данными-в-момент-маунта-виджета)
      - [Получение локального стейта виджета](#получение-локального-стейта-виджета)
  - [Добавить виджет на существующую страницу ПИ](#добавить-виджет-на-существующую-страницу-пи)

## Принципы работы

- Виджет считается самостоятельной клиентской единицей.
- Виджеты работают **только** с:
    - нормализованными данными из `state.collections`
    - собственным изолированным стейтом

## Файловая структура

```
partnernode/client.next/pidgets/
├── UniqueName/     # Уникальное имя виджета
│   ├── View.js     # Корневой реакт компонент
│   ├── actions.js  # Приватные экшены виджета
│   ├── epics.js    # Эпики
│   ├── index.js    # Файл с объявлением виджета
│   ├── reducer.js  # Редюсер
│   └── state.js    # Объявление типа redux стейта и генерируемой им функции
├── README.md       # Документация
├── root.js
└── style.css
```

```typescript
// client.next/pidgets/Foobar/state/index.js

export type State = {};
export const makeInitialState = () => {/* начальное состояние виджета */};
```

### Экшены виджета

Описывать экшени и экшен креейторы можно любым удобным способом. У нас есть `typed-actions`, `rainbow-actions` или руками.

### Объявление виджета

Виджет объявляется с помощью `PidgetUtil`. Виджет должен быть экспортирован [именованным экспортом](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export#using_named_exports) (`export const Foobar = ...`).

```typescript
// client.next/pidgets/Foobar/index.js

import {PidgetUtil} from '~/pidgets/root'

import {View, type ViewProps} from './View'
import {reducer} from './reducer'
import * as epics from './epics'
import {makeInitialState, type State} from './state';

export const Foobar = PidgetUtil.createPidget<State, ViewProps>(
    {
        View,
        name: 'Foobar',
        makeInitialState,
        reducer,
        epics,
    }
)
```

### State виджета

```typescript
// client.next/pidgets/Foobar/state/index.js

export type State = {};
export const makeInitialState = (): State => {/* начальное состояние виджета */};
```

### Редюсер виджета

Аналогично привычным редюсерам, можно использовать `typed-actions`, писать руками, `redux-toolkit`, you name it

```typescript
// client.next/pidgets/Foobar/index.js

import {handleActions, type Handlers} from 'typed-actions/immer'
import {BAR, type Actions} from './actions'
import {makeInitialState, type State} from './state'

export const reducer = handleActions(
    {
        [BAR]: (state, {payload}) => {
            state.thing = payload
        },
    }: Handlers<State, Actions>,
    makeInitialState(),
)
```

### View и вложенные компоненты

Пишутся так же как в основном проекте, за исключением приведённых правил

- Для получения по селектору данных из стейта виджета используется `useSelector` или `useSelectorSafe` из `~/pidgets/root`
- Для получения состояния виджета используется `usePidgetStatus` из `~/pidgets/root`
- Для получения общего стора(кроме ветки `page`) используется `useAppStateSelector` из `~/pidgets/root`
- Для `dispatch`'а нужно использовать `useDispatch` из `~/pidgets/root`, а не из `react-redux`
-  `useAction` нужно брать из `~/pidgets/root`, а не из `~/hooks/redux` 
- Нельзя ходить в сторы других виджетов
- Нельзя ходить в стор страницы (`state.page`)

Если следовать этим правилам, ваш виджет будет самостоятельным и его можно будет свободно переиспользовать между страницами.

### Epics виджета

В эпиках мы работает с сайдэффектами, такими как загрузка данных для отрисовки виджета. Все эпики виджета можно разобрать на 3 типа

1. [Работа с данными для маунта виджета](#работа-с-данными-для-маунта-виджета)
1. [Работа с данными в момент маунта виджета](#работа-с-данными-в-момент-маунта-виджета)
1. Все остальные про ворклоу виджета

Стоит обратит внимание на первые 2 типа. В обоих случаях мы сначала проверяем есть ли нужные виджету данные в сторе и если нет, запрашиваем.


#### Работа с данными до маунта виджета

Если то что будет нарисовано виджетом никак не зависит от внешних параметров(пропсов), значит мы можем запросить эти данные до того как сам виджет будет отрисован. Это значит что мы можем подписать на экшен инициализации приложения и положить туда нашу логику

```typescript
// client.next/pidgets/Foobar/epics.js

import {from, of} from 'rxjs';
import {mergeMap, catchError} from 'rxjs/operators';
import {ofType} from 'redux-observable';
import ctx from '@yandex-market/mandrel/clientContext';
import {type Actions, INIT_PAGE} from '~/actions/app';
import {type Actions, updateCollections} from '~/actions/collections';

import {resolveFoobarPidgetData} from 'shared/resolvers';

export const premountEpic = (action$, store$) => action$.pipe(
    ofType(INIT_PAGE),
    withLatest(store$),
    mergeMap(([, state]) => {
        const isPidgetDataReady = getIsFoobarPidgetDataReady(state);

        /**
         * Если все данные уже есть, ничего не делаем,
         * в момент отрисовки виджет сам получит все данные и отрисует
         */
        if (isPidgetDataReady) {
            return EMPTY;
        }

        /**
         * В противном случае идём за данными
         */
        return from(resolveFoobarPidgetData(ctx)).pipe(
            mergeMap(response => of(
                /**
                 * Поскольку пиджет еще не замаунтился, его стора еще нет в редаксе,
                 * а значит данные могут находиться только в общих коллекциях
                 */
                updateCollections(response),
            )),
            catchError(error => of(logError({type: 'request', error}))),
        );
    }),
);
```

#### Работа с данными в момент маунта виджета

```typescript
// client.next/pidgets/Foobar/epics.js

import {from, of} from 'rxjs';
import {mergeMap, catchError} from 'rxjs/operators';
import {ofType} from 'redux-observable';
import ctx from '@yandex-market/mandrel/clientContext';
import {onPidgetMount} from '~/pidgets/root';
import {type Actions, updateCollections} from '~/actions/collections';
import {updateFoobarState} from './actions';

import {resolveFoobarPidgetData} from 'shared/resolvers';

export const onPidgetMountEpic = (action$, store$) => action$.pipe(
    onPidgetMount('Foobar'),
    withLatest(store$),
    mergeMap(([{props}, state]) => {
        /**
         * Можно подсмотреть внешние пропс виджета из экшена
         */
        const isPidgetDataReady = getIsFoobarPidgetDataReady(state, props);

        /**
         * Если все данные уже есть(были получены ранее/виджет отрисовывается не в первый раз),
         * можно ничего не делать
         */
        if (isPidgetDataReady) {
            return EMPTY;
        }

        /**
         * В противном случае идём за данными
         */
        return from(resolver(resolveFoobarPidgetData(ctx, toParams(props)))).pipe(
            mergeMap(response => of(
                /**
                 * Общие данные отправляем в коллекции
                 */
                updateCollections(response.colleactions),
                /**
                 * Приватные данные отправляем в изалированный стор виджета
                 */
                updateFoobarState(response.anotherPart),
            )),
            catchError(error => of(logError({type: 'request', error}))),
        );
    }),
);
```

#### Получение локального стейта виджета

- для получения полного состояния пиджета(value + type) используется `withLatestPidgetState`
- если в эпике нужен только value пиджета, используется `mapWithPidgetValue`

## Добавить виджет на существующую страницу ПИ

Внутри страницы используются как обычные react компоненты

```diff
// client.next/pages/MYPAGE/components/Comp.tsx

import React from 'react';
import {Column} from '@yandex-levitan/b2b';

+import {Bar} from '~/pidgets/Bar';
+import {Foo} from '~/pidgets/Foo';

export const Comp = ({propA, propB}) => (
    <Column>
+        <Bar propA={propA} />
+        <Foo propB={propB} />
    </Column>
);
```
