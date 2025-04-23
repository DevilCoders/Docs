
Задает обработчик onClick компонента <a href='@self/platform/components(src)/Link'>Link</a> поведением <a href='@self/platform/components(src)/Hoc'>withPageChangeHandler</a> (клиентский роутинг, метрика navigate).

Набор параметров определяется как совокупность параметров <a href='@self/platform/components(src)/Link'>Link</a> и хока <a href='@self/platform/components(src)/Hoc'>withPageChangeHandler</a>.

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;

    const store = createStore(() => ({
        collections: {},
    }));

    const route = {pageId: 'bm:order', params: {orderId: 1}};
    const url = 'http://yandex.ru';

    <Provider store={store}>
        <div>
            <div>
                <Link back>Ссылка назад (клиентский роутинг)</Link>
            </div>
            <div>
                <Link route={route} anchor>Ссылка на route (клиентский роутинг)</Link>
            </div>
            <div>
                <Link route={route}>Ссылка на route с метрикой</Link>
            </div>
            <div>
                <Link url={url}>Ссылка на url с метрикой(не рекомендуется - лучше route)</Link>
            </div>
        </div>
    </Provider>
```
