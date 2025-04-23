# Redux

Связано c: [withReduxState](../../components/withReduxState/README.md)

## Мотивация

Необходимо между разными компонентами шарить данные. Делать это через какой-нибудь родительский `<GoodObject />` – не получится:
- Пока нет множественной гидрации, все дочерние компоненты будут наследовать `{ hasClient: true }`, что не всегда это надо
- Т.к. страницы должны строиться из `turbo-json`, использовать одну точку входа и рендерить весь реакт не получится
- Еще есть `bem` компоненты, которые охота малыми усилиями пока поддержать

Так же охота:
- Отделить бизнес-логику от компонента

## Общее

- Интерфейс
  - получает данные
  - генерирует события
  - не знает, что за собой влечет событие
  - структура страницы должна быть гибкой (избежать завязки на вложенность компонент)
- Бизнес-логика
  - принимает сигналы
  - обновляет данные
  - выполняет все, что необходимо (походы в бэкенд, работа с browser API...)
  - не имеет представления, как это выглядит интерфейсно
  - логика должны быть кастомизируемой под отдельный сервис


## Идея

- Компоненты подключаются к `redux` через `withReduxState` + `selectors` + `actions`
- В адаптерах пушим скрипт, который
  - добавляет `reducers`
  - подписывается на `action.type`
  - отправляет `actions`
  - взаимодействует с различными api (backend, browser)



## Реализация

Реализация лежит в
- [core/state/store.ts](./store.ts) - клиентская часть
  - [getStore](#getstore-source)
  - [registerReducer](#registerreducer-source)
  - [registerActionSubscriber](#registeractionsubscriber-source)
  - [resetStore](#resetstore-source)
  - [getReducers](#getreducers-source)

- [assets.ts](../assets/store.js) - на сервере
  - [context.assets.pushStore](#contextassetspushstore-source)

---

### getStore ([source]())

```ts
function getStore<T>(): Store<T, IAnyAction>
```

> Метод доступен в `window.Ya.getStore`

Создает инстанс `store`, кладет его в `window.Ya.store`.

`<T>`, формат куска `store`, который будет использоваться. Например: `getStore<{ cart: ICartData }>()`

---

### registerReducer ([source](./store.ts#L49))

```ts
function registerReducer(key: string, reducer: Reducer): void
```

> Внутри вызывается `getStore`, отдельно инитить ее не требуется

Подключает кастомный `reducer` в корень `store`

- `key` – ветка в корне `store`
- `reducer` - стандартный reducer для этой ветки

---

### registerActionSubscriber ([source](./store.ts#L71))

```ts
function registerActionSubscriber(actionType: string, handleDispatch: TActionSubscriber): void
```

> При вызове этого метода, наличие самого `store` не обязательно

Подписка на события в `redux`, за место дополнительного `eventEmitter`. Реализованно с помощью простой `middleware` - `actionSubscriberMiddleware`


- `actionType` – событие, которое приходит через `dispatch`.
- `handleDispatch` – колбэк на это событие, который будет выполнен после изменения `state`. В колэке можно реализоывать свою бизнесс логику, которая будет, например, ходить на бэкенд, слать дополнительно экшены.

``type TActionSubscriber = (store: MiddlewareAPI, action: IAnyAction) => void;``

---

### resetStore ([source](./store.ts#L130))

```ts
function resetStore<T>(initialState?: DeepPartial<T>): void
```

Обнуляет `store`. При следующем `getStore` будет создан следующий инстанс с `initialState`

---

### getReducers ([source](./store.ts#L146))

```ts
function getReducers(): record<string, Reducer>
```

 Функция нужна для таких вещей как `<Store />`, в которой динамическое добавление `reducers` реализованно отдельно

---

### context.assets.pushStore ([source](https://github.yandex-team.ru/serp/turbo/blob/dev/platform/types/AdapterContext.ts#L186))

```ts
function pushStore<T>(chunk: DeepPartial<IGlobalState | T>): void;
```

Добавляет часть данные в `initialState`, которые будут доставленны на клиент.

Функция доступная в контекста адаптеров

> ВАЖНО: Сейчас есть спецэффект связанный с тем, что `store` будет инитится с этими данными, но `reducer` для ветки еще не добавлен

Пример:
```ts
// ./Component.adapter.ts

this.context.assets.pushStore<{ cart: IState }>({
    cart: {
        shopId: data.shopId,
        loading: true,
        meta: data.meta,
    }
});
```

### Начало использования


## Проблемы
