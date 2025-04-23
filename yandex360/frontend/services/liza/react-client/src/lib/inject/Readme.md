# `lib/inject`

DI-фреймворк, основанный на токенах.
Наш подход к внедрению зависимостей достаточно нетипичен — мы хотим создавать сущности при запросе их из инжектора двумя способами:
1. Возвращать один и тот же экземпляр класса для одного набор параметров (например, для моделей, по аналогии с noscript'ом)
2. Всегда создавать новый экземпляр (например, для процессов, которые не имеют состояния и хранить их экземпляры в кеше инжектора бессмысленно)

Общим ограничением нашего DI-фреймворка является работа с конструкторами строго с одним аргументом, вида
```typescript
class MyType {
    constructor(props: { foo: string; bar: BarType }) {
    }
}
```

## Указываем, как создавать экземпляры нашего типа

Для указания того, как создавать тип используются Токены. В текущем варианте существуют Токены двух видов:
- `SingletonToken()` скажет инжектору возвращать один и тот же экземпляр для одного набора параметров
- `AlwaysNewToken()` — создавать новый инстанс каждый раз и не хранить его в кеше

Поскольку токен связан с конкретным типом, да ещё и с его декорируемым вариантом, который неизвестен при определении класса, токены используют позднее связывания — тип будет зафиксирован при первом получении токена из контекста вызова `this`.
Посему токены являются функциями, записанными в статические свойства на типе класса, например
```typescript
class MyAwesomeType {
    static Token = SingletonToken()
}
```

Наш инжектор очень хитёр и умеет строит иерархии типов с пропами, выводя пропы зависимостей из пропов класса, который их хочет получить.
Работает это примерно так
```typescript
class MyParentType {
    // Здесь мы должны указать, каким образом из пропов типа `MyParentType`
    // посчитать не-инжектируемые пропы типа `MyChildType`
    static Token = SingletonToken(props => ({
        child: MyChildType.Token({
            foo: props.bar,
        })
    }));

    constructor(props: { bar: string, child: MyChildType }) {
    }
}

class MyChildType {
    // Здесь мы указываем, что проп `other` будет браться из инжектора,
    // а проп `foo` надо будет передать при инстанциировании
    static Token = SingletonToken({
        other: SomeOtherType.Token() // Тип определён где-то ещё, за пределами примера :)
    });

    constructor(props: { foo: string, other: SomeOtherType }) {
    }
}
```

## Инжектим зависимости в компонент

Для внедрения зависимостей в реакт-компонент используется HoC [`withInject()`](./withInject.tsx).

В самом простом виде достаточно объявить хэш зависимостей
```typescript
class MyType {
    static Token = AlwaysNewToken();

    constructor(private props: { title: string }) {
    }

    public get title(): string {
        return this.props.title;
    }
}

const MyComponent: React.FC<{ myType: MyType }> = props => (
    <div>{ props.myType.title }</div>
);

export const WrappedComponent = withInject({
    myType: MyType.Token({ title: 'Dude' }),
})(MyComponent);
```

HoC позволяет вычислить пропы зависимостей от пропов компонента, продолжим предыдущий пример
```typescript
interface Props {
    title: string;
}

const MyOtherComponent: React.FC<Props & { myType: MyType }> = props => (
    <div>{ props.myType.title }</div>
);

// Здесь свойство `title` для внедрения в `MyType` будет взято из пропов компонента
export const WrappedOtherComponent = withInject((props: Props) => ({
    myType: MyType.Token({ title: props.title }),
}))(MyOtherComponent);
```

## Получаем экземпляр из инжектора (плохая идея 😉)

> Получать экземпляры напрямую из инжектора обычно не следует, но есть ряд сценариев, таких, как интеграция со старым приложением, где без этого не обойтись.

Если требуется получить экземпляр какого-то класса внутри типа, который сам инстанциируется через инжектор (имеет Token), следует использовать тип  `InjectorInstance`
```typescript
class MyType {
  public static readonly Token = SingletonToken(MyType, {
    injector: InjectableInstance.Token()
  });

  constructor(private params: { injector: InjectableInstance }) {
  }

  public method() {
    this.params.injector.Instance(OtherType.Token());
  }
}
```

В случаях, где надо получить экземпляр внутри слоя, который ничего про инжектор не знает, *⚠️ как карйнюю меру* можно использовать напрямую статический класс [`lib/inject/Inject#Injector`](./Inject.ts).

```typescript
Injector.Instance(MyType.Token({
    param1,
    param2
}))
```
