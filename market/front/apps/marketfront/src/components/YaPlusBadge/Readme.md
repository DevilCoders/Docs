### Песочница
```jsx noeditor
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    let store = createStore(() => {});

    <Provider store={store}>
        <Helper.Playground component={YaPlusBadge} />
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
            <YaPlusBadge />
            
            <h3>Все размеры обычной темы</h3>
            <hr />

            <div style={style}><YaPlusBadge theme='gradient' size='xs'/></div>
            <div style={style}><YaPlusBadge theme='gradient' size='s'/></div>
            <div style={style}><YaPlusBadge theme='gradient' size='m'/></div>
            <div style={style}><YaPlusBadge theme='gradient' size='l'/></div>

            <h3>Все размеры черной темы</h3>
            <hr />

            <div style={style}><YaPlusBadge theme='black' size='xs'/></div>
            <div style={style}><YaPlusBadge theme='black' size='s'/></div>
            <div style={style}><YaPlusBadge theme='black' size='m'/></div>
            <div style={style}><YaPlusBadge theme='black' size='l'/></div>

            <h3>Все размеры белой темы light</h3>
            <hr />

            <div style={style}><YaPlusBadge theme='white' size='xs'/></div>
            <div style={style}><YaPlusBadge theme='white' size='s'/></div>
            <div style={style}><YaPlusBadge theme='white' size='m'/></div>
            <div style={style}><YaPlusBadge theme='white' size='l'/></div>
        </div>
    </Provider>
```
