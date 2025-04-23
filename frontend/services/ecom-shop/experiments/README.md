# Эксперименты в TAP

### Пример заведения эксперимента

Допустим, мы хотим внедрить экспериментальный компонент `ExperimentalCounter`.

Для начала нам нужно, как обычно, завести сам exp flag `my-experimental-counter`.
Далее, в папке `experiments` нужно завести директорию по имени эксперимента.
В этой директории будут лежать как сами экспериментальные компоненты, так
и необходимые для эксперимента матчеры и логика по управлению состоянием приложения.
Структура директорий должна иметь следующий вид:
```
├── experiments
│   ├── my-experimental-counter
│   │   ├── components
│   │   ├── matchers
│   │   ├── redux
```

#### Заводим матчеры

В эксперименте нам могут понадобиться какие-то особые данные,
которые приходят в turboJson и которые повлияют на начальное
состояние приложения. Реализация экспериментальных матчеров
ничем не будет отличаться от реализации обычных:
```typescript
// experiments/my-experimental-counter/matchers/parseProductCard.ts

import { IEcomBlock } from '../../../types';
import { IMapBlocksToMatchers } from '../../types';
import { TAppState } from '../redux';
import { validatePath } from '../../../turbojsonParser/utils';

export const metaMatch = (node: IEcomBlock, result: TAppState) => {
    if (!validatePath(node, 'doc')) {
        return;
    }

    result.meta.myExperimentalCounter = node.meta.myExperimentalCounter;
};

export const mapBlocksToMatchers: IMapBlocksToMatchers = {
    meta: metaMatch,
};
```

В переменной `mapBlocksToMatchers` ключами обязательно должны быть
имена блоков, которые будут встречаться в turboJson.

Так как для каждой страницы у нас свой набор матчеров, в эксперименте
так же необходимо указать эту информацию:
```typescript
// experiments/my-experimental-counter/matchers/index.ts

import { EEcomPage } from '../../../turbojsonParser/types';
import { IMatchersByPage } from '../../types';
import { mapBlocksToMatchers as productCardMatchers } from './parseProductCard';

const matchersByPage: IMatchersByPage = {
    [EEcomPage.ProductCard]: productCardMatchers,
};

export default matchersByPage;
```

#### Модифицируем логику по управлению состоянием приложения

Всю необходимую логику по управлению состоянием можно положить в
директорию `redux` в папке эксперимента. Аналогично, структура
файлов в этой директории будет повторять базовую. В нашем
эксперименте мы хотим хранить дополнительное поле в `meta`:

```typescript
// experiments/my-experimental-counter/redux/meta/reducer.ts

import { Reducer } from 'redux';
import { IAppState, IData } from '../../../../types';

export type TMetaState = IAppState['meta'] & {
    myExperimentalCounter: number;
}

export const metaReducer: Reducer<TMetaState> = (state, action) => {
    switch (action.type) {
        case '@@meta/INCREASE_COUNTER':
            return {
                ...state,
                myExperimentalCounter: state.myExperimentalCounter + action.payload,
            };
        default:
            return {
                ...state,
            };
    }
};
```

Также необходимо указать к каким полям стора будут относиться новые
экспериментальные редьюсеры и описать интерфейс состояния стора:
```typescript
// experiments/my-experimental-counter/redux/index.ts

import { IAppState } from '../../../types';
import { metaReducer, TMetaState } from './meta/reducer';

export type TAppState = IAppState & {
    meta: TMetaState,
}

export const reducers = {
    meta: metaReducer,
};
```

Так как начальное состояние экспериментального поля не
всегда получится вычислять из парсеров, необходимо описать
получение начального состояния:
```typescript
// experiments/my-experimental-counter/redux/meta/reducer.ts

// ...
import { getInitialState as getBaseInitialState } from '../../../../redux/services/meta/reducer';

// ...
export const getInitialState = (): TMetaState => {
    const baseInitialState = getBaseInitialState();

    return {
        ...baseInitialState,
        myExperimentalCounter: 0,
    };
};
```

Опишем функцию получения начального состояния
всех полей стора эксперимента:
```typescript
// experiments/my-experimental-counter/redux/meta/reducer.ts

import { getInitialState as getMeta } from './meta/reducer';

export function getInitialState() {
    return {
        meta: getMeta(),
    };
}
```

#### Реализуем экспериментальные компоненты
Тот компонент, который будет подгружаться динамически, в своей
реализации ничем не будет отличаться от обычных. Единственное, что
нужно сделать дополнительно - это задекларировать его как динамический:
```typescript
// experiments/my-experimental-counter/components/ExperimentalCounter/index.ts

import * as Loadable from 'react-loadable';

export const ExperimentalCounter = Loadable({
    loader: () => import(
        /* webpackChunkName: "experiment-counter" */
        './ExperimentalCounter')
        .then(module => {
            return module.ExperimentalCounter;
        }),
    loading: () => null,
    modules: ['./Actions'],
    webpack: () => [require.resolveWeak('./Actions') as number],
});
```

Здесь `ExperimentalCounter` это обертка над реальным компонентом,
которая умеет загружать его по требованию. Про опции, которые можно
передавать в `Loadable`, можно почитать [тут](https://github.com/jamiebuilds/react-loadable#loadable-and-loadablemap-options).

Обязательным является указание `/* webpackChunkName: "experiment-counter" */`
с уникальной строкой `counter` (среди других динамических компонентов)
и префиксом `experiment-`, так как требуется соглашение по именованию
для реализации серверного рендера таких динамических компонентов.

#### Декларирование эксперимента
Далее эксперимент нужно задекларировать:
```typescript
// ...
import myExperimentalCounter from './my-experimental-counter';

export default {
    // ...
    'my-experimental-counter': {
        redux: myExperimentalCounter.redux,
        matchers: myExperimentalCounter.matchers,
    },
};
```
В объекте, который будет доступен по одинаковому с именем
эксперимента ключу, ожидаются поля `redux` и `matchers`. В
объекте в поле `redux` ожидаются поля `reducers` и `getInitialState`.

После реализации всего, что необходимо для эксперимента, должна была
получиться примерно следующая структура файлов:
```
├── experiments
│   ├── my-experimental-counter
│   │   ├── components
│   │   │   ├── ExperimentalCounter
│   │   │   │   ├── ExperimentalCounter.tsx
│   │   │   │   ├── index.tsx
│   │   ├── matchers
│   │   │   ├── index.ts
│   │   │   ├── parseProductCard.ts
│   │   ├── redux
│   │   │   ├── meta
│   │   │   │   ├── reducer.ts
│   │   │   ├── index.ts
│   │   │   ├── initialState.ts
```
