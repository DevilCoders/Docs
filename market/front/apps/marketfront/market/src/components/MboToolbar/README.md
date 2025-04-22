# MboToolbar

Тулбар в сниппете продукта/оффера на выдаче для контентщиков

```jsx
const {createStore} = require('redux');
const {Provider} = require('react-redux');
const MboToolbar = require('@self/platform/components/MboToolbar').default;
const {offer} = require('@self/platform/components/MboToolbar/__fixtures__');

const store = createStore((store) => store, {
    collections: {
        mboComplain: {},
    },
});

<Provider store={store}>
    <MboToolbar
        canUserComplainOfClassifier
        entity={offer}
    />
</Provider>
```
