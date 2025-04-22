# `lib/middleware`

Набор middleware для [`Dispatcher`'а](../dispatch).


## `ActionMiddleware`

Action'ы работают похожим на redux образом — конкретная модель может объявить список action'ов с которыми собирается работать в виде наследников типа `Action` и мутировать своё состояние, получая новый изменённый стейт от reducer'а.

Поскольку экземпляров одной модели, созданных с разными параметрами может быть много, каждый action, объявленный для данного типа, прольётся через все экземпляры модели.
Определить, на какой именно экземпляр action будет влиять — задача логики reducer'а.

> В примере ниже используется HoC `withInject()`. Подробнее про него можно почитать в документации к модулю [`lib/inject`](../inject)

В общем случае, использование выглядит как
```typescript
class IncrementAction extends Action<{ amount: number }> {
}

class DecrementAction extends Action<{ amount: number }> {
}

const actions = new Actions<CounterModel>()
    .on(IncrementAction, (state, action) => ({
        count: state.count + action.amount,
    }))
    .on(DecrementAction, (state, action) => ({
        count: state.count - action.amount,
    }));

@StaticModel(actions)
class CounterModel {
    public count = 0;
}

// Дальше где-то в приложении
withInject({ dispatcher: Dispatcher.Token() })(props => {
    const increment = useCallback(
        () => props.dispatcher.dispatch(new IncrementAction({ amount: 2 })),
        [props.dispatcher],
    );

    return (
        <button onClick={ increment }>Increment</button>
    );
});
```

## `ProcessMiddleware`

Процессы — сущность, выполняющая функции похожие на thunk'и в redux'е — это место для бизнес-логики и описания конкретных сценариев.

Рассмотрим пример с `Action`'ами выше и обернём это в процесс.
```typescript
enum EventType {
    INCREMENT,
    DECREMENT,
}

// Этот тип процесс получит в конструкторе и присвоит в `this.params`
interface Params {
    event: EventType;
    amount: number;
    dispatcher: Dispatcher;
}

class UpdateCounterProcess extends Process<Params> {
    public async run(): Promise<void> {
        const { dispatcher, event, amount } = this.params;

        if (event === EventType.INCREMENT) {
            return dispatcher.dispatch(new IncrementAction({ amount }));
        }

        return dispatcher.dispatch(new DecrementAction({ amount }));
    }
}

// И дальше изменим реализацию нашего компонента
withInject({ dispatcher: Dispatcher.Token() })(props => {
    // Для этого примера мы передадим Dispatcher в процесс параметром конструктора.
    // Так делать не стоит, более правильным будет объявление зависимостей
    // и использование inject-middleware
    const increment = useCallback(
        () => props.dispatcher.dispatch(new UpdateCounterProcess({
            event: EventType.INCREMENT,
            amount: 2,
            dispatcher: props.dispatcher,
        })),
        [props.dispatcher],
    );

    return (
        <button onClick={ increment }>Increment</button>
    );
});
```

Скорее всего, большая часть процессов захочет работать с `Dispatcher`'ом, поэтому будет использоваться через `inject`-middleware, описанную ниже.


## `InjectMiddleware`

Не добавляет отдельных сущностей, вместо этого позволяет dispatch'ить `InjectionToken`'ы, по которым создаются сущности через `Injector`.
Это частый случай с процессами (см. `Process` middleware выше), которым требуются зависимости, но может работать для любого типа, которому потребуются injectable-зависимости.

Для наглядности вернёмся к примеру из секции `Process` middleware и перепишем его с использованием токена процесса вместо создания экземпляра вручную.

```typescript
// --- Типы параметров остаются без изменений

class UpdateCounterProcess extends Process<Params> {
    // Нет смысла хранить в кеше экземпляр процесса, поскольку тот не имеет состояния,
    // поэтому используем `AlwaysNewToken()`
    public static readonly Token = AlwaysNewToken(UpdateCounterProcess, {
        dispatcher: Dispatcher.Token(),
    });

    public async run(): Promise<void> {
        const { dispatcher, event, amount } = this.params;

        if (event === EventType.INCREMENT) {
            return dispatcher.dispatch(new IncrementAction({ amount }));
        }

        return dispatcher.dispatch(new DecrementAction({ amount }));
    }
}

withInject({ dispatcher: Dispatcher.Token() })(props => {
    // Теперь мы будем dispatch'ить токен вместо экземпляра процесса, всю работу по созданию
    // сущности и разрешению зависимостей за нас выполнит inject middleware
    const increment = useCallback(
        () => props.dispatcher.dispatch(UpdateCounterProcess.Token({
            event: EventType.INCREMENT,
            amount: 2,
        })),
        [props.dispatcher],
    );

    return (
        <button onClick={ increment }>Increment</button>
    );
});
```

## `NsBridgeMiddleware`

Служит для отправки event'ов и action'ов в noscript.
Определяет два типа action'ов:
- `NsEvent` — dispatch такого action'а отправит noscript-event
- `NsAction` - dispatch отправит noscrip-action

Используется как и другие action'ы
```typescript
class DoSomeNsStuff extends NsAction<{ foo: string }> {
    name = 'some.stuff';
}

class SendSomeNsEvent extends NsEvent<{ bar: string }> {
    name = 'event.name';
}

declare const dispatcher: Dispatcher; // откуда-то получили

dispatcher.dispatch(new DoSomeNsStuff({
    node, // опциональный параметр — связанная DOM-нода
    event, // опциональный параметр — связанное DOM-событие
    foo: 'bar',
}));

dispatcher.dispatch(new SendSomeNsEvent({
    bar: 'baz',
}));
```

## Отладка

`ActionMiddleware`, `ProcessMiddleware`, `NsBridgeMiddleware` интегрируются с redux-dev-tools через сервис [`DevTools`](../devtools/DevTools.ts).

![Redux Dev Tools screenshot](./devtools.png)
