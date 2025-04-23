# Client

**client.next** собирается только вебпаком и выполняется только в браузере. Тут не должно быть обращений к встроенным модулям nodejs.

- [react](#react)
- [redux](#redux)
- [RxJS](#rxjs)

## React

- [docs](https://reactjs.org/docs/hello-world.html)

Полезное:
  - [Как мы пишем код на `React`](#сode)
  - [redux](#redux)
  - [Производительность реакт-приложений (@enload)](http://slides.com/lttb/react-perf#/)

### Code

На данный момент основная структура проекта следующая:
- actions
- components
- config
- containers
- [epics](#epics)
- pages
  - {PageName}
    - actions
    - components
    - epics
    - [reducers](#pagespagenamereducers)
    - [selectors](#pagespagenameselectors)
    - [types](#pagespagenametypes)
    - [App.js](#pagespagenameappjs)
    - [index.js](#pagespagenameindexjs)
- reducers
- types
- utils

#### Components

При написании Компонентов и их логики мы используем подход, который можно назвать `HOC-way UI Architecture`. Это значит, что
- React Компонент – **отображение**
- HOC - **UI логика**

Такой подход дает нам следующие бенефиты:
- Высокая реиспользуемость как логики, так и отображения
- Раздельное тестирование логики и отображения
- Композируемость логики
- и кое-что еще

Большинство HOC'ов мы используем из библиотеки [recompose](https://github.com/acdlite/recompose/blob/master/docs/API.md).

> Подробнее можно посмотреть в докладе [Как Партнерские Интерфейсы переехали на Реакт](https://youtu.be/uIM6m62_MWU)

Таким образом каждый Компонент имеет следующую структуру:

```jsx
import React from 'react'

type Props = { /* ... */ }

/**
 * Не забываем называть Компоненты правильно
 */
const MyComponent = (props: Props) => (
  /* React Element */
)

/**
 * Не забываем указать тип HOC
 */
export const enhance: HOC<*, { /* ... */ }> = compose(
  /* список хоков */
)

/**
 * Иногда композиция не нужна, в таком случае делаем так:
 *
 * export const enhance = withSomething
 *
 * Обратите внимание, что здесь уже указывать тип не нужно - он должен быть у withSomething и так.
 */

/**
 * Презентационный Компонент мы экспортируем под названием Base
 * В 99.99% случаев это должно быть использовано только в тестах.
 *
 * Если же презентационный компонент реиспользуемый и сильно абстрагирован от логики, то он должен быть вынесен отдельно и экспортироваться as is.
 */
export {MyComponent as Base}

/**
 * По умолчанию экспортируем декорированный Компонент
 */
export default enhance(MyComponent)
```

В одном файле может быть описано несколько презентационных Компонентов, но только один усилитель и соответствующий дефолтный экспорт. Поэтому если какому-то из дополнительных Компонентов также требуется усилитель, то его необходимо вынести в отдельный файл с той же, описанной выше, структурой.

Tips:

- Базовые понятия в контексте HOC - это внешний (Enhanced) и внутренний (Base) интерфейс Компонента. Внешний - это интерфейс для пользователей Компонента (например, передача пропсов при создании реакт элемента). Внутренний - это то, что Компонент уже получит в виде пропсов. Любой хок может быть описан следующим типом:
  ```js
  type HOC<Base, Enhanced> = ComponentType<Base> => ComponentType<Enhanced>
  ```

- Хоки именуются как `withSomething`. Желательно, чтобы `Something` отражало изменение пропсов, например, `withStyles` добавляет `styles` во внешний интерфейс, `withUser` добавляет `user` во внутренний и т.д.

- *Когда нужен HOC, а когда нет?*
- HOC - это про **логику**. То есть это описание хендлеров, UI стейта Компонента и так далее. Кроме того, это про **интерфейс** - влияние как на внешний (Enhanced), так и на внутренний (Base) интерфейс Компонента. В подавляющем большинстве случае композиция хоков - это пайплайн преобразований пропсов Компонента. То есть презентационной части/нод-врапперов в хоках быть не должно, не считая крайних случаев. Например, так делать **не надо**:
  ```jsx
  const withProvider = Comp => props => <Provider><Comp {...props} /></Provider>
  ```

  Правильнее будет обернуть Компонент во враппер `Provider` уже непосредственно в самой верстке.

- *Как определить react lifecycle (или любое другое, что требует класс)*?
- У `recompose` есть HOC под названием `lifecycle`, однако его использовать не стоит. Лучше определить класс с нужными методами, например:
  ```jsx
  const withSomething = <Props>(
    cp: (Props) => void
  ) => (Comp: ComponentType<Props>) => class extends Component<Props> {
    componentWillMount() {
      cb(this.props)
    }
    render() { return <Comp {...this.props} /> }
  }
  ```

- *Зачем нужно типизировать хоки?*
- Основной недостаток, и в то же время преимущество хоков - это преобразование единых пропсов компонента. Таким образом возможны конфликты, затирание значений, непредсказуемость конечных данных и так далее. Однако это актуально в случае, если нет типизации. Когда же типизация есть, то такая проблема решается автоматически (тайп-система скажет вам, если есть конфликтующие пропсы и покажет конечные типы), при этом такой подход обеспечивает дополнительную согласованность интерфейсов.

- *Чем отличается паттерн `render-props` и когда какой нужен?*
- `render-props` позволяет обеспечить удобное взаимодействие между родительским и дочерним Компонентами. Это своего рода **dependency injection** в дочерний Компонент. Действительно, хоки часто можно выразить через `render-props`, и часто в интернете можно встретить такие преимущества над хоками вроде инкапсуляции. Действительно, в некоторых случаях это важно, однако главная область применения хоков - это как раз композиционность **преобразований интерфейсов и поведения** Компонента, а указанная проблема конфликтующих пропсов решается типами (см. предыдущий пункт). Но в случае с **DI** `render-props` - удобный паттерн. Пример реализации - новый `React Context Api`. При этом композиция `render-props` компонентов уже довольно печальная, хотя есть решения.

- *Как их тестировать?*
- Смотри [тут](https://github.yandex-team.ru/market/b2b-components/tree/master/src/spec/mocks)

- *Как использовать connect?*
- В большинстве случаев `connect` определяется следующим образом:
  ```js
  connect(
    (state) => { /* данные из стейта */ },
    {actionCreator1, actionCreator12, /* ... и т.д. */ }
  )
  ```

  Если же нужно вызвать какой-то экшн по, например, клику, то использовать `recompose` не стоит, для избежания создания лишних оберток для компонента. Для этой цели отлично подойдет 3ий аргумент `connect`'а:
  ```js
  const enhance: HOC<InnerProps, OuterProps> = (
    (state) => { /* данные из стейта */ },
    {action1},
    (mappedProps, dispatchedProps, ownProps): InnerProps => ({
        ...mappedProps,
        onClick: event => dispatchedProps.action1(event.currentTarget.value)
    })
  )
  ```

  Это нужно для инкапсуляции логики стейта и методов работы с ним уже относительно компонентов. Такой подход позволяет вынести подобные коннекты в реиспользуемую часть логики, абстрагировавшись от способов работы с экшнами внутри Компонентов. (`action1` может быть вызван по клику, по вводу, по движению мыши и так далее).

- *Как избежать лишних ререндеров?*
- Информация есть тут (стоит посмотреть): [Производительность реакт-приложений (@enload)](http://slides.com/lttb/react-perf#/). Из основных вещей - это `pure` Компоненты. Для этого есть класс `React.PureComponent`, либо, в контексте ХОКов, - хок `pure` из `recompose` (см. также `onlyUpdateForKeys` и т.д.). Также потребуется [reselect](https://github.com/reactjs/reselect) для мемоизации селекторов из стейта.

##### Использование React Hooks

Вместо библиотеки `recompose` можно и нужно использовать [React Hooks](https://reactjs.org/docs/hooks-intro.html).

Плюсы хуков:
 - В большинстве случаев автоматическая типизация, с `recompose` тип пропсов приходится указывать вручную;
 - Красивое дерево компонентов в React Devtools;
 - С 2018 года recompose находится на поддержке, новые фичи не разрабываются.
 
С хуками по-прежнему нужно отдельно хранить отображение и UI логику.

Рассмотрим разницу в двух подходах на примере компонента-кнопки. Текст достается из стора, при клике должен выстреливать экшн. А еще пусть кнопка исчезает, как только на нее нажали.

```jsx
import React from 'react'
import {compose, withHandlers, withStateHandlers, branch, renderNothing} from 'recompose';
import {connect} from 'react-redux';

import {getButtonText} from '~/pages/MyPage/selectors';
import {doSomethingOnClickAction} from '~/pages/MyPage/actions';

const MyComponent = ({handleClick, text, isButtonVisible}: Props) => (
    <Button onClick={handleClick}>
      {text}
    </Button>
);

const mapStateToProps = (state: State) => ({
    text: getButtonText(state),
});

const mapDispatchToProps = {
    doSomethingOnClick: doSomethingOnClickAction,
};

const enhance: HOC<Props, {||}> = compose(
    connect(
        mapStateToProps,
        mapDispatchToProps,
    ),
    withStateHandlers(() => ({isButtonVisible: true}), {
        setIsButtonVisible: () => value => {
            return {
                isButtonVisible: value,
            };
        },
    }),
    withHandlers({
        handleClick: ({doSomethingOnClick, setIsButtonVisible}) => () => {
            doSomethingOnClick();
            setIsButtonVisible(false);
        },
    }),
    branch(({isButtonVisible}) => !isButtonVisible, renderNothing),
);

export default enhance(MyComponent);
```

В React Devtools мы увидим вот такого монстра:
![дерево для компонента с recompose](https://jing.yandex-team.ru/files/dariaborisyak/uhura_2020-12-16T23%3A23%3A19.790469.jpg)

А вот как будет выглядеть тот же самый компонент, написанный при помощи хуков:

```jsx
import React, {useCallback, useState} from 'react';
import {useDispatch, useSelector} from 'react-redux';

import {getButtonText} from '~/pages/MyPage/selectors';
import {doSomethingOnClickAction} from '~/pages/MyPage/actions';

// Вся логика по получению пропсов уходит в кастомный хук
function useEnhance() {
    const dispatch = useDispatch();
    
    const text = useSelector(getButtonText);
    const [isButtonVisible, setIsButtonVisible] = useState(true);
    const handleClick = useCallback(() => {
        dispatch(doSomethingOnClickAction());
        setIsButtonVisible(false);
    }, [dispatch, setIsButtonVisible]);
    
    return {isButtonVisible, handleClick, text};
}

export function MyComponent() {
    const {isButtonVisible, handleClick, text} = useEnhance();
    if (!isButtonVisible) return null;
    
    return (
        <Button onClick={handleClick}>
            {text}
        </Button>
    );
}
```

Здесь `useEnhance` выступает в роли привычного энханса, который подготавливает все данные для вьюшной части. В итоге из всего файла экспортируется только `MyComponent`.


**О непереиспользуемых компонентах**

Если компонент не будет переиспользоваться, можно применять хуки прямо внутри него, без дополнительных оберток:

```jsx
export const MyComponent = () => {
    const {someProp} = useSelector(getSomeProp);
    const {someOtherProp} = useSelector(getSomeOtherProp);
    
    return (
        <>
          {someProp}
          {someOtherProp}
        </>
    );

```
Но если во view-компоненте больше двух хуков, их лучше вынести в кастомный хук.

**Когда использовать `useCallback`**  

Использование `useCallback` для мемоизации хендлеров на каких-то примитивных компонентах не имеет большого смысла, так как эти компоненты в любом случае чаще всего не мемоизированные и ререндерятся и так. При этом сложности коду это добавляет.

`useCallback` стоит определять, когда хендлер используется в качестве пропсов у **мемоизированного** компонента (например, контейнера), когда эта оптимизация действительно нужна.

Рассмотрим пример:
```jsx
const Cars = ({cars}) => {
  const onCarClick = carId => {
    const car = cars.find(({id}) => id === carId);
    console.log(car.model);
  }
  
  return cars.map((car) => {
    return (
      <Car id={car.id} onCarClick={onCarClick} key={car.id} />
    )
  });
}
```

При этом `Car` - мемоизированный компонент:

```jsx
const Car = React.Memo(...);
```

Здесь на каждый рендер компонента Cars у нас создается новая функция onCarClick - соответственно, все компоненты Car всегда будут заново рендериться, т.к. каждый раз получают новую ссылку на функцию.
В этом случае имеет смысл использовать `useCallback`:
```jsx
const Cars = ({ cars }) => {
  const onCarClick = useCallback(carId => {
    const car = cars.find(({id}) => id === carId);
    console.log(car.model);
  }, [cars]);
  
  return cars.map((car) => {
    return (
      <Car id={car.id} onCarClick={onCarClick} key={car.id} />
    )
  });
}
```
Теперь компоненты Car не будут рендериться лишний раз, т.к. ссылка на функцию останется прежней.

**Тестирование компонентов с хуками**

Компоненты можно тестировать через мок функции useEnhance. Это позволяет не воссоздавать моки под стор и все остальные хуки, а тестировать вью-компонент в разных изолированных состояниях. Это можно сделать разными вариантами, самый простой, с помощью https://github.com/speedskater/babel-plugin-rewire/.
Сам хук `useEnhance` стоит протестировать, если он содержит в себе нетривиальную логику.

**<a id="hook-to-backend" name="hook-to-backend"></a> Общение с бекендом в хуках**

Для начала нужно ознакомиться с [epics](#epics). Ниже описан метод общения с бекендом через хуки React, но при применении этого метода следует помнить, что методом по умолчанию для общения с бекендом являются всё-таки epics.

Иногда есть ситуации, когда получать данные через epic слишком накладно по отношению к использованию этих данных. Например, если по клику на кнопку нужно сходить в бек, получить сумму и отрисовать её вместо кнопки, и нигде в другом месте эта сумма использоваться не будет, то можно реализовать логику обращения к беку в кастомном хуке, чтобы не усложнять код приложения лапшой из epic/action/reducer.

Пример для понимания ситуации:
```tsx
// useGetSum.ts

export const useGetSum = ({someId}: {someId: SomeID}) => {
  const [status, setStatus] = useState<Status | undefined>();
  const [sum, setSum] = useState<number | undefined>();
  const dispatch = useDispatch();

  // Обнуляемся при смене someId.
  useEffect(() => {
    setStatus(undefined);
    setSum(undefined);
  }, [someId]);

  const startGetSum = useCallback(() => {
    setStatus(STATUS.pending);
    getSumResolver(ctx, {someId})
      .then(({sum}) => {
        setStatus(STATUS.done);
        setSum(sum);
      })
      .catch(() => {
        dispatch(showError({type: 'while-getting-sum'}));
        setStatus(STATUS.error);
      });
  }, [someId]);

  return {
    sum,
    sumStatus: status,
    startGetSum,
  };
};

// MyComponent.tsx

export const MyComponent = ({someId}: {someId: SomeID}) => {
  const {sum, status, startGetSum} = useGetSum({someId});
  if (status !== STATUS.done) {
    return (
      <Button state={status === STATUS.pending ? 'pending' : 'normal'} onClick={startGetSum}>
        Получить сумму
      </Button>
    );
  }
  return <RenderSum sum={sum} />;
}
```

Но в таком, казалось бы, простом коде можно натолкнуться на проблемные места сейчас и в будущем:
- Непонятно, где должна происходить обработка ошибки получения суммы - должен ли хук сам это делать, должен делегировать компоненту или пробрасывать в epic через специальный action?
- Нужно не забыть вообще обработать ошибку получения суммы понятным для пользователя образом.
- Как рефакторить этот код, если сумма понадобится в нескольких местах?
- Cостояние и данные у нас хранятся в хуке, и достать их для дебага будет проблематично.

Коллегиально на встрече "Беседы про ПИ" были выработаны следующие правила обращения к бекенду через хуки:
- можно обращаться к беку через хуки, если все условия выполняются:
  - происходит операция чтения данных (get);
  - данные прокидываются только вниз по дереву компонентов через пропсы;
- нельзя обращаться к беку через хуки, и нужно использовать epic/state, если выполняется хотя бы одно условие:
  - выполняется модификация сущностей на беке (post/put/patch/иногда-и-get), т.е. вызов бека меняет что-то в магазине/бизнесе/etc;
  - данные нужно использовать в нескольких местах на странице, и как минимум одно из них находится в другом поддереве компонент;
  - при обработке данных нужно модифицировать state;
- существующее обращение к беку через хуки нужно переписать на epic/state, если выполняется хотя бы одно условие:
  - данные понадобились в другом поддереве компонент;
  - понадобилось модифицировать state;

ВАЖНО! Даже если ваш код соответствует критериям "можно написать поход в бек черех хук", перед написанием кода всё-таки лучше подумать и сформулировать причины, по которым стандартный метод похода в бекенд (epic/actions/reducers/state) не подходит, и записать эти причины в отдельном комментарии в описании хука, чтобы другие разработчики могли ознакомиться с контекстом ситуации.

#### pages/{PageName}/reducers

- [Про редьюсеры](#reducers)

Редьюсеры страницы.
Корневой файл экспортирует редьюсеры верхнего уровня, а также конечный стейт страницы, описанный с помощью `RootState` и стейтов импортированных редьюсеров. Про то, как писать сами редьюсеры, можно почитать [здесь](#reducers).

> `combineReducers` на **этом этапе** делать **не нужно**, так как они будут скомбинированы с остальными корневыми редьюсерами при конфигурации (`~/config`).

Пример `index.js`:
```js
import type {RootState} from '~/reducers';
import page, {type State as PageState} from './page';

type AppState = {
  params: {
    fromDate: string,
    toDate: string,
  },
};

export type State = RootState<AppState, PageState>;

export {page};
```

#### pages/{PageName}/types

Здесь должны быть описаны сущности и реиспользуемые типы. Также отсюда экспортируется тип `State` страницы, который в дальнейшем будет использоваться в Компонентах, эпиках и т.д.

Пример `index.js`:
```js
export type {State} from '../reducers'

export type A = { ... }
```

#### pages/{PageName}/App.js

Декларация корневого контейнера страницы. Здесь собирается итоговое view приложения.

Пример:
```jsx
import React from 'react';

import A from './components/A';
import B from './components/B';

const App = () => (
    <>
        <A />
        <B />
    </>
);

export default App;
```

#### pages/{PageName}/selectors

Селекторы для вашей страницы, тут должны лежать селекторы только для обращения в ветки `page` из redux стора. Селекторы для других веток стора стоит искать в `~/selectors/<branch-name>` или завести соответственный, если такого файла не существует.

Селекторы стоит писать составные и по возможности переиспользуемые. Смотри пример ниже

```js
// pages/{PageName}/selectors.js

import type {EntityId, Entity, State} from 'shared/pages/{PageName}';

/**
 * так делать НЕ стоит ❌
 */

export const getEntityById = (state: State, entityId: EntityId): ?Entity => state.page.entities.find(entity => entity.id === entityId);

/**
 * так делать СТОИТ ✅
 */

export const getEntities = (state: State): Entity[] => state.page.entities;

export const getEntityById = (state: State, entityId: EntityId): ?Entity => getEntities(state).find(entity => entity.id === entityId);
```

#### pages/{PageName}/index.js

Конфигурация страницы. Важно следовать конвенции именования `App` и `config` соответственно.

Пример:
```js
/* @flow */

import render from '~';
import Config from '~/config';

import * as reducers from './reducers';
import * as epics from './epics';

import App from './App';

const config = Config({
    epics,
    reducers,
});

render(App, config);
```

### Redux

- [docs](https://redux.js.org/)
- dev-инструменты:
  - [расширение для браузера](http://extension.remotedev.io/)

- [actions](#actions)
- [reducers](#reducers)
- [epics](#epics)

#### actions

Actions определяются с помощью `createActions` из [typed-actions](#typed-actions). Например:

```js
import {createActions, action, empty} from 'typed-actions';

/**
 * Значение экшн типа определяется следующим образом:
 *
 * const ACTION = 'namespace/anotherNamespace/.../ACTION'
 *
 * Состояния экшна могут быть представлены так (с помощью суффиксов):
 *
 * ACTION
 * ACTION_FULFILLED
 * ACTION_FAILED
 * ACTION_CANCELLED
 */
export const UPDATE = 'page/statOrders/UPDATE';
export const UPDATE_FULFILLED = 'page/statOrders/UPDATE_FULFILLED';
export const UPDATE_FAILED = 'page/statOrders/UPDATE_FAILED';

let actions;

/**
 * Мапинг на экшн креаторы
 */
export const {
    [UPDATE]: update,
    [UPDATE_FULFILLED]: updateFulfilled,
    [UPDATE_FAILED]: updateFailed,
} = actions = createActions({
    [UPDATE]: empty,
    /**
     * Достаточно указать только тип аргументов. Если же payload не нужен, но надо использовать функцию `empty`
     */
    [UPDATE_FULFILLED]: (x: string) => action(x),
    [UPDATE_FAILED]: empty,
});

/**
 * Экспортируем Тип Коллекции экшн креаторов.
 */
export type Actions = typeof actions;
```

Tips:

- Экшны стоит декомпозировать по файлам. Например:
  ```js
  /* actions/namespace/index.js */

  export * from './a'
  export * from './b'

  /* actions/namespace/a.js */

  export const A = 'base/namespace/A'
  export const A_FAILED = 'base/namespace/A_FAILED'

  /**
   * Определяем экшн креаторы и т.д.
   */

  /* actions/namespace/b.js */

  export const B = 'base/namespace/B'
  export const B_FAILED = 'base/namespace/B_FAILED'

  /**
   * Определяем экшн креаторы и т.д.
   */
  ```

#### reducers

Reducers определяются с помощью `handleActions` из [typed-actions](#typed-actions). Например:

```js
import {handleActions, type Handlers} from 'typed-actions';

import {UPDATE, type Actions} from 'actions';

/**
 * Определяем и экспортируем участок State, с которым будут работать редьюсеры.
 */
export type State = {
    data: {a: number},
};

export default handleActions(({
    [UPDATE]: (state, payload) => ({...state, data: payload}),
}: Handlers<State, Actions>));
```

Tips:

- Редьюсеры стоит декомпозировать по файлам. Например:
  ```js
  /* reducers/namespace/index.js */

  import a, {type State as AState} from './a'
  import b, {type State as BState} from './b'

  export type State = {
    a: AState,
    b: BState,
  }

  export default combineReducers({a, b})

  /* reducers/namespace/a.js */

  import {type Actions, A} from 'actions'

  export type State = { ... }

  export default handleActions(...)

  /* reducers/namespace/b.js */

  import {type Actions, B} from 'actions'

  export type State = { ... }

  export default handleActions(...)
  ```

#### epics

Используем `redux-observable`.

- [docs](https://redux-observable.js.org/)

Используется для работы с сайдэффектами. Работает на основе [RxJS](#rxjs).
Основная определяемая сущность - `epic`. В данном контексте `epic` - это описание реакции и сайдэффектов на экшн. Эпик может подписываться как на один экшн, так и на несколько, например (все названия вымышленные и называть эпики нужно **осмысленно**):

```js
/**
 * Импортируем тип Epic, который является доопределением типа из `typed-actions/redux-observable`
 */
import type {Epic} from '~/types/redux'

/**
 * Импортируем стейт страницы
 */
import type {State} from '~/pages/{PageName}/types'

/**
 * Импортируем тип Коллекции экшн-креаторов и сами экшн-креаторы
 */
import {type Actions, A, a, B, b} from '~/pages/{PageName}/actions'

export const AEpic
  : Epic<State, Actions>
  = (action$) => action$
    .ofType(A) // выбираем нужные экшны
    /*... */ // делаем нужные преобразования

export const ABEpic
  : Epic<State, Actions>
  = (action$) => action$
    .ofType(A, B)
    /*... */ // В данном случае в операторы попадет экшн уже типа A | B
```

Tips:

- Эпики стоит декомпозировать по файлам. Например:
  ```js
  /* epics/namespace/index.js */

  export * from './a'
  export * from './b'

  /* epics/namespace/a.js */

  export const nameSpaceA1Epic ...
  export const nameSpaceA2Epic ...

  /* epics/namespace/b.js */

  export const nameSpaceB1Epic ...
  export const nameSpaceB2Epic ...
  ```

- *Когда использовать эпики?*
- Когда нам нужно упаковать сайдэффект, таким образом не нарушая чистоту экшн-креаторов или редьюсеров. Чаще всего это про поход в какие-либо ручки, однако, есть и другие кейсы. Например, есть две коллекции: заказы и пользователи. Где-то в приложении пользователь выбирает определенный заказ, и мы диспатчим экшн вроде `SELECT_OFFER`. Мы бы могли при диспатче экшна в контейнере или где-то еще положить в пейлоад данные выбранного заказа, однако в таком случае нам придется это делать каждый раз при использовании этого экшн-креатора, хотя эти данные могут быть и не нужны в конкретном контексте. Поэтому в данном случае вместо дублирования логики прокидывания данных заказа можно указать `id` выбранного заказа, то есть диспатчить экшн наподобие `{type: SELECT_OFFER, payload: {offerId}}`, и уже **в эпике** получить нужный заказ из коллекции. Таким образом логика работы с данными заказа будет определена в одном месте без размазывания ее по приложению.

- *Что такое `map`, `mergeMap`, `flatMap`, `switchMap` и когда что использовать?*
- Начнем с того, что `mergeMap` и `flatMap` - это алиасы, так что в их поведении разницы нет. В случае, например, с `map` мы должны вернуть просто данные, тогда как для `flatMap`/`switchMap` мы возвращаем также стрим (к примеру, это актуально когда мы работаем с `api`). Для того, чтобы понять, с каким данными работает каждый оператор, нужно посмотреть на его сигнатуру в документации или типах. Отличие `flatMap` и `switchMap` в том, что второй оператор прекращает работу предыдущего стрима. Рассмотрим следующие ситуации:
  ```js
  export const AEpic
    : Epic<State, Actions>
    = (action$) => action$
      .ofType(A)
      .mergeMap(action => api(...).map(c)) // c - экшн креатор

  export const BEpic
    : Epic<State, Actions>
    = (action$) => action$
      .ofType(B)
      .switchMap(action => api(...).map(c)) // c - экшн креатор
  ```

  `AEpic` среагирует на каждый экшн `A`, и в результате задиспатчит экшн `c`. И важно, что он будет диспатчить **каждый** результат выполнения. Таким образом, даже если предыдущий вызов `api` был дольше, чем самый последний, тогда, когда он будет зарезолвен, будет диспатч экшна `c`, что может привести к неожиданным последствиям. В случае же с `BEpic` на каждый `B` предыдущий стрим будет отменен (причем даже на уровне запроса к бэкенду - будет аборт и `http` запроса в данном случае, что тоже хорошо), таким образом будет диспатч `c` после запроса данных только для последнего экшна. Поэтому чаще всего **для работы с `api`** стоит использовать **именно `switchMap`**.

Про обработку ошибок и их отображение в клиентском логгировании, можно прочитать [https://wiki.yandex-team.ru/users/alantukh/market/error-booster/](тут).

#### typed-actions

- [docs](https://github.com/lttb/typed-actions)

Аналог [redux-actions](https://github.com/redux-utilities/redux-actions), но в контексте системы типов [flow](#flow). Предоставляет расширенные возможности для покрытия типами `actions/reducers/epics` с автовыводом.

## RxJS

- [docs](http://reactivex.io/rxjs/)

Полезное:
- еще одна доступная [документация](https://www.learnrxjs.io/)
