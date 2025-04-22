# Reducktor

Эта библиотека позволяет разделять ваш redux-стор на отдельные модули, которые в дальнейшем будут именоваться "утки" (ducks).

Есть два варианта создания уток.

## createSimpleDuck

```ts
const createUserDuck = createSimpleDuck((options) => ({
    actions: {
        action1: (state, payload) => newState,
        action2: (state, payload) => newState,
    },
    selectors: {
        selector1: (state) => selectorResult,
    },
    initialState,
}));
```

Фабрика должна вернуть объект, где:
* actions - мапа из имен экшенов и редьюсеров
* selectors - мапа селекторов
* initialState - начальный стейт

## createDuck

```ts
const createUserDuck = createDuck((options) => {
    return {
        reducer,
        actions,
        selectors,
    };
});
```

-   reducer - обычный редьюсер
-   actions - мапа из имен экшенов и actions creators
-   selectors - мапа из имен селекторов и самих селекторов, **которые принимают на вход стейт самой утки.**

Первый способ является предпочтительным, в нём минимум боилерплеита и не требуются внешние зависимости.
Просьба новые возможности реквестить или хотя бы ставить в ревью @eduarddyckman

## создание инстанса утки

```ts
const userDuck = createUserDuck('user', options);
```

В конструктор утки передаются два параметра:

-   ключ утки, с которым она будет подключена в стор
-   (опционально) опции, которые будут переданы в фабрику утки

## что есть в инстансе утки

```ts
assert.isEqual(userDuck.actions.setUserName(userName), {
    type: 'user/setUserName',
    payload: userName,
});
assert.isEqual(userDuck.selector(state), userDuckState);
assert.isEqual(userDuck.selectors.userName(state), 'Vasily'); // передётся глобальный стейт!
assert.isEqual(
    userDuck.reducer(state, userDuck.actions.setUserName('Vasily')),
    { ...state, userName: 'Vasily' },
);
assert.isEqual(userDuck.key, 'user');
```

### подключение к стору

```ts
import * as ducks from './ducks';
const { store, dispose } = createStoreFromDucks(ducks, {
    saga: rootSaga,
    state: initialState,
    middlewares: [metrikaCounter()],
});
```
