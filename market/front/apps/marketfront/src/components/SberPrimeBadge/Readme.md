### Песочница
```jsx noeditor
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    let store = createStore(() => {});

    <Provider store={store}>
        <Helper.Playground component={SberPrimeBadge} />
    </Provider>
```

### Примеры
```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;

    let store = createStore(() => {});

    const style = {marginTop: 10};

    <Provider store={store}>
        <div>
            <SberPrimeBadge />

            <h3>Все размеры обычной темы</h3>
            <hr />

            <div style={style}><SberPrimeBadge size='s'/></div>
        </div>
    </Provider>
```
