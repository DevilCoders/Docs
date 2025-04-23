# Использование React

Официальная документация: https://reactjs.org/docs/react-api.html

## Шпаргалка по созданию компонентов

```tsx
// Инициализация хелпера для построения имен классов.
const b = bevis('my-component');

interface Props {}

interface State {}

interface Snapshot {}

class MyComponent extends React.Component<Props, State, Snapshot> {
    // displayName пишем только для connector'ов, в остальных случаях он генерируется автоматически при сборке.
    static displayName = '';

    private _somePrivateProp?: number;
    private _ref = React.createRef<HTMLDivElement>();
    private _elementRef = React.createRef<HTMLElement>();

    constructor(props: Props) {
        super(props);

        this.state = {}; // Начальное состояние компонента.
    }

    static getDerivedStateFromProps(nextProps: Props, prevState: State): Partial<State> | null {}
    componentDidCatch(error: Error, errorInfo: ErrorInfo): void {}

    // @see https://reactjs.org/docs/react-component.html#lifecycle-methods
    componentDidMount(): void {}
    shouldComponentUpdate(nextProps: Props, nextState: State): boolean {}
    componentDidUpdate(prevProps: Props, prevState: State, snapshot?: Snapshot): void {}
    componentWillUnmount(): void {}
    getSnapshotBeforeUpdate(prevProps: Props, prevState: State): Snapshot | null {}

    // Для всех приватных методов также указываем тип возвращаемого значения.
    private _onSomething = (): void => {};
    private _onSomethingElse = (): void => {};

    // Функция должна быть без сайд-эффектов.
    render(): React.ReactNode {
        const props = this.props;
        return (
            <div className={b()} ref={this._ref}>
                <span className={b('element')}></span>
                <span className={b('element-with-state', {collapsed: true})}></span>
                <ChildComponent />
                <ChildComponentWithTonsOfProps {...passPropsFromObject} />

                <ChildComponentWithTonsOfProps
                    stringProp="value"
                    booleanProp
                    numberProp={111}
                    objectProp={{foo: 'bar'}}
                    functionProp={this._onSomething}
                >
                    <span>child</span>
                </ChildComponentWithTonsOfProps>

                <ChildComponentWithChildren>
                    <span></span>
                </ChildComponentWithChildren>
            </div>
        );
    }
}
```

В случае простых компонент рекомендуется использовать stateless functional components:

```tsx
interface Props {}

const MyComponent: React.FunctionComponent<Props> = (props) => {
    return <div className={b()} />;
};
```

## Mount/unmount

-   Любой компонент, добавленный в DOM через `ReactDom.render`, должен быть удален через `ReactDom.unmountComponentAtNode`. Удаления родительской DOM-ноды не достаточно для правильной очистки ресурсов.

## Рекомендации

-   Оставлять метод `render` максимально простым.

1. Никаких сайд-эффектов.
2. Создавать как можно меньше новых объектов, функций и т.п. внутри метода.
3. Выносить из метода все расчеты, которые не зависят от `state` и `props`.
4. Все вспомогательные методы компонента `private`

-   Не изменять `this.state` напрямую:

```tsx
// Плохо:
this.state.isCollapsed = !this.state.isCollapsed;
this.setState(this.state);

// Хорошо:
this.setState({isCollapsed: !this.state.isCollapsed});
```

-   Не добавлять в `this.state` значения, которые могут быть вычислены (из `props` или из других значений, хранящихся в `state`)

```tsx
// Плохо:
this.setState({isPositive: this.props.num > 0});

// Хорошо:
render: function (): React.ReactNode {
    const isPositive = this.props.num > 0;
    // ... some use of isPositive
}
```

-   Избегать сильной вложенности в tsx:

```tsx
// Плохо:
return (
    <Child1>
        <Child2>
            {props.list.map((item) => (
                <Child3>
                    <Child4>
                    </Child4>
                </Child3>
            ))}
        </Child2>
    </Child1>
);

// Возможные решения: выносить в отдельные переменные, функции или компоненты.
const items = (
    {props.list.map((item) => (
        <Child3>
            <Child4>
            </Child4>
        </Child3>
    ))}
);

return (
    <Child1>
        <Child2>
            {items}
        </Child2>
    </Child1>
);

return (
    <Child1>
        <Child2>
            {props.list.map(renderItem)}
        </Child2>
    </Child1>
);

return (
    <Child1>
        <Child2>
            {props.list.map((item) => <Item key={item.id} item={item} />)}
        </Child2>
    </Child1>
);
```

-   Использовать `this._something = ...` только в исключительных случаях для хранения состояния,
    которое не должно напрямую влиять на представление.
    По умолчанию всё состояние должно находиться либо в `props`, либо в `state`.

-   Использовать `shouldComponentUpdate` только в исключительных случаях, в которых очень важна производительность.
    По умолчанию для уменьшения количества лишних апдейтов достаточно использовать [PureComponent](https://reactjs.org/docs/react-api.html#reactpurecomponent)

-   В качестве inline условий используется только тернарный оператор:

```tsx
// Хорошо:
{
    condition ? <View /> : null;
}
```

```tsx
// Плохо:
{
    condition && <View />;
}
```

-   `ReactRedux.connect` описывается перед компонентом, чтобы находиться как можно ближе к декларации Props (поскольку, чаще всего они изменяются вместе).

## References

[Рекомендуемым способом](https://reactjs.org/docs/refs-and-the-dom.html) использования ссылок на DOM-элементы является `createRef` API.

Для использования API нужно создать объект типа `React.RefObject` с помощью `React.createRef<T>()`, где `T extends HTMLElement`.

В сложных случаях возможно использование callback API.
