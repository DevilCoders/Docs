# Динамические импорты

[Динамический импорт](https://webpack.js.org/api/module-methods/#import-1) позволяет загружать код в браузер только тогда, когда будет нужна соответствующая функциональность. Частные случаи — это функциональность "за кликом" или "колбаски".

### Пример

Компонент [Username](../../../src/experiments/learn_serp_dynamic_imports/features/Greeting/Greeting.components/Username/Username.tsx) подключается в конструкторе [Greeting](../../../src/experiments/learn_serp_dynamic_imports/features/Greeting/Greeting@desktop.tsx):

``` tsx
constructor() {
    super({});

    import('./Greeting.components/Username/Username').then(
        ({ Username }) => {/* ... */})
    );
}
```

Сначала `Greeting` отрендерит текст `'Как дела, ?'` без обращения к пользователю:

``` tsx
state = { Username: () => null };

render() {
    const { Username } = this.state;

    return <div className="Greeting">Как дела, <Username />?</div>;
}
```

Когда рантайм webpack-а загрузит код компонента `Username`, можно через `setState` запустить перерисовку:

``` tsx
import('./Greeting.components/Username/Username').then(
    ({ Username }) => this.setState({ Username })
);
```

### react-loadable

Стандартный паттерн, использованный в примере выше, используется очень часто. На практике его чаще используют через [react-loadable](https://github.com/jamiebuilds/react-loadable).

Переписанный пример:

``` tsx
import Loadable from 'react-loadable';

const UsernameLoadable = Loadable({
    loader: () => import('./Greeting.components/Username/Username'),
    loading: () => null,
    render: ({ Username }) => <Username />,
});

export const GreetingPresentor = () => (
    <div className="Greeting">Как дела, <UsernameLoadable />?</div>
);
```

Пример использования `react-loadable` в проекте можно увидеть в компоненте [MMModalAsync](../../../src/components/MMModalAsync).
