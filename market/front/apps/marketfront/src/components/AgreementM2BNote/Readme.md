Условия покупки и доставки на сервисе

```jsx
    import AgreementNote from '@self/root/src/components/AgreementM2BNote';

    import {Provider} from 'react-redux';
    import {createStore} from 'redux';
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <Helper.Playground
            component={AgreementNote}
            defaultValues={{buttonText: 'Подтвердить заказ'}}
        />
    </Provider>
```
