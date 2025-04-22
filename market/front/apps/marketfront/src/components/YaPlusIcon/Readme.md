### Песочница
```jsx noeditor
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    let store = createStore(() => {});

    <Provider store={store}>
        <Helper.Playground component={YaPlusIcon} />
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
            <YaPlusIcon />

            <h3>Все размеры</h3>
            <hr />

            <div style={style}><YaPlusIcon size='xxs'/></div>
            <div style={style}><YaPlusIcon size='xs'/></div>
            <div style={style}><YaPlusIcon size='s'/></div>
            <div style={style}><YaPlusIcon size='m'/></div>
            <div style={style}><YaPlusIcon size='l'/></div>
            <div style={style}><YaPlusIcon size='xl'/></div>
            <div style={style}><YaPlusIcon size='xxl'/></div>
            
            <h3>Все темы</h3>
            <hr />

            <div style={style}><YaPlusIcon theme='logo-white' /></div>
            <div style={style}><YaPlusIcon theme='logo-black' /></div>
            <div style={style}><YaPlusIcon theme='logo-gradient' /></div>
            <div style={style}><YaPlusIcon theme='glyph-black' /></div>
            <div style={style}><YaPlusIcon theme='glyph-white' /></div>
        </div>
    </Provider>
```
