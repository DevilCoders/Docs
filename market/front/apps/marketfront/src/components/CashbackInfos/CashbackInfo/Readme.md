Баллы Кэшбэка по Яндекс Плюсу

### Песочница
```js noeditor
const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;

let store = createStore(() => {});

// Взято из @self/root/src/uikit/components/Text, todo поддержать TypoSize, TypoWeight
const sizes = 'default,800,700,600,500,400,350,300,250,200,100'.split(',');
const weights = 'regular,medium,bold'.split(',');

<Provider store={store}>
    <Helper.Playground
        component={CashbackInfo}
        settings={{background: 'transparent'}}
        defaultValues={{value: 1000}}
        props={{
            textSize: {
                type: 'enum',
                required: false,
                values: sizes,
            },
            weight: {
                type: 'enum',
                required: false,
                values: weights,
            },
        }}
    />
</Provider>
```
