# Готовые примеры как писать юнит-тесты на Jest

* Мы пишем юнит-тесты на [jest](https://jestjs.io)
* Тесты пишутся в файле `file.test.js`
* При написании тестов мы используем следующую нотацию:
  * `describe()` для создания сьюта
  * `it()` для создания теста
  * `expect()` для проверки утверждения
* Не надо создавать верхоуровневый сьют, если он повторяет смысл самого файла (тестируем модуль X). Если в сьюте проверяется какие-то аспекты работы модуля, то можно.
* Описание тестов и сьютов пишем на русском языке

## http/ajax запросы

Юнит-тесты ни в коем случае не должны ходить по http на удаленные сервера. Все запросы надо мокать.
Иначе такой тест будет нестабильным из-за неправильного окружения, недоступности бекенда и т.д.

### gateApi

Можно мокать ответы на уровне gateApi

```
// мокаем модуль gateApi
jest.mock('auto-core/react/lib/gateApi', () => {
    return {
        getResource: jest.fn(),
    };
});

const getResource = require('auto-core/react/lib/gateApi').getResource;

it('тест с ajax-запросом', () => {
   // ...

   // реализуем нужный для теста ответ
   getResource.mockImplementation(() => Promise.resolve());

   // expect(...)
});
```

### fetch()

`global.fetch` глобально замокан через [jest-fetch-mock](https://github.com/jefflau/jest-fetch-mock).
Поэтому в тестах можно писать вот так

```
beforeEach(() => {
    // сбрасываем мок перед каждым тестом
    fetch.resetMocks();
});

it('fetch mock example', async () => {
    fetch.mockResponseOnce(JSON.stringify({ status: 'ERROR' }));

    // ... какой-то тест, который вызывает fetch ... //
});
```

### http-запросы в nodejs

Такие запросы на мокать через [nock](https://github.com/nock/nock).

## React, Redux

### actions, reducer, store

Экшены и редьюсеры можно тестировать просто как функции, тогда ничего специфичного не требуется.

```
it('пример теста для экшена', () => {
    expect(myAction()).toEqual({ type: 'MY_TYPE', payload: {} });
});

it('пример теста редьсера', () => {
    expect(reducer(state, action)).toEqual({ foo: 'bar' });
});
```

Но лучше тестировать экшены (особенно, если они асинхронные) или редьюсеры в связке с store.

```
// подключаем redux-mock-store
const mockStore = require('autoru-frontend/mocks/mockStore').default;

// пересоздаем store на каждый test
let store;
beforeEach(() => {
    store = mockStore({
        listing: {
            data: {
                search_parameters: {
                    mark_model_nameplate: [ 'AUDI#100' ],
                },
            },
        },
    });
});

it('пример синхронного экшена', () => {
    // массив экшенов, которые должны были произойти в сторе
    const expectedActions = [
        { type: LISTING_CHANGE_PARAMS, payload: {
            mark_model_nameplate: [ 'AUDI#100' ],
            price_from: 1000,
        } },
    ];

    // отправляем событие в store
    store.dispatch(changeParams({ price_from: 1000 }));
    expect(store.getActions()).toEqual(expectedActions);
});

it('пример асинхронного экшена', async () => {
    // массив экшенов, которые должны были произойти в сторе
    const expectedActions = [
        { type: LISTING_CHANGE_PARAMS, payload: {
            mark_model_nameplate: [ 'AUDI#100' ],
            price_from: 1000,
        } },
    ];

    // отправляем событие в store
    await store.dispatch(changeParams({ price_from: 1000 }));
    expect(store.getActions()).toEqual(expectedActions);
});
```

### redux connect

```
const React = require('react');
const { Provider } = require('react-redux');
const renderer = require('react-test-renderer');

const mockStore = require('autoru-frontend/mocks/mockStore').default;

it('должен протестировать компонент с connect()', () => {
    // мокаем нужное состояние в store
    const store = mockStore({
        geo: {},
        listing: {
            data: {
                search_parameters: {
                    section: section,
                },
            },
        },
    });

    // рендерим компонент, используя обычный <Provider> из react-redux
    const tree = renderer.create(
        <Provider store={ store }><ListingCarsH1/></Provider>
    ).toJSON();
    expect(tree).toMatchSnapshot();
});
```

### this.context

Для тестирования компонентов с `context` есть мок `createContextProvider`, который может эмулировать любой контекст.

```
const React = require('react');
const renderer = require('react-test-renderer');

const createContextProvider = require('autoru-frontend/mocks/createContextProvider').default;

it('должен правильно отрендерить компонент с this.context.link', () => {
    const link = jest.fn(() => '/card-link');
    const ContextProvider = createContextProvider({ link });

    const tree = renderer.create(
        <ContextProvider>
            <MyComponent/>
        </ContextProvider>
    ).toJSON();
    expect(tree).toMatchSnapshot();
});
```

### snapshot testing

[Документация](https://jestjs.io/docs/en/snapshot-testing)

**Важно**: 
1. Файлы снапшотов (`__snapshots__/file.test.js.snap`) **НАДО коммитить** в репозитарий. Иначе тестам будет не с чем сравнивать.

1. Снепшоты сложно проверять и поддерживать, поэтому подумай, можно ли обойтись без них. Если нужно что-то проверить в вёрстке: пропы или порядок компонентов, лучше делать это точечно, а саму вёрстку проверять скриншотными тестами. 

### как замокать методы любого объекта (например global aka window)

```js
beforeEach(() => {
    jest.spyOn(global, 'addEventListener').mockImplementation(...);
});

afterEach(() => {
    jest.restoreAllMocks();
});
```
