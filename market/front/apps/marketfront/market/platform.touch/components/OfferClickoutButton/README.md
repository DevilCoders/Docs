```jsx
const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;
const store = createStore(() => {});

<Provider store={store}>
    <div style={{width: '300px'}}>
        <OfferClickoutButton
            buy={{
                type: 'clickout',
                url: 'https://yandex.ru',
            }}
            shopId={774}
        />
    </div>
</Provider>
```
