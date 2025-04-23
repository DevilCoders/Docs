Новый/уцененный товар

Пример использования:
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const initialState = {
    discountList: [
        {
            id: '1',
            value: 'new',
            isChecked: false,
            priceMin: {
                currency: 'RUR',
                value: '1000',
            },
        }, {
            id: '2',
            value: 'cutprice',
            isChecked: false,
            priceMin: {
                currency: 'RUR',
                value: '500',
            },
        }
    ]
};

const [state, setState] = React.useState(initialState);

<Provider store={store}>
    <DiscountFilter
        discountList={state.discountList}
        onChange={({value}) =>
            setState({
                discountList: state.discountList.map(el => {
                    if (el.value === value) {
                        return {...el, isChecked: true};
                    }
        
                    return {...el, isChecked: false};
                })
            })
        }
    />
</Provider>
```

Без цен:
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const initialState = {
    discountList: [
        {
            id: '1',
            value: 'new',
            isChecked: false,
            priceMin: {
                currency: 'RUR',
                value: '1000',
            },
        }, {
            id: '2',
            value: 'cutprice',
            isChecked: false,
            priceMin: {
                currency: 'RUR',
                value: '1500',
            },
        }
    ]
};
const [state, setState] = React.useState(initialState);

<Provider store={store}>
    <DiscountFilter
        discountList={state.discountList}
        onChange={({value}) =>
            setState({
                discountList: state.discountList.map(el => {
                    if (el.value === value) {
                        return {...el, isChecked: true};
                    }
        
                    return {...el, isChecked: false};
                })
            })
        }
    />
</Provider>
```

C disabled:
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const initialState = {
    discountList: [
        {
            id: '1',
            value: 'new',
            isChecked: false,
            priceMin: {
                currency: 'RUR',
                value: '1000',
            },
        }, {
            id: '2',
            value: 'cutprice',
            isChecked: false,
            priceMin: {
                currency: 'RUR',
            },
        }
    ]
};
const [state, setState] = React.useState(initialState);

<Provider store={store}>
    <DiscountFilter
        discountList={state.discountList}
        onChange={({value}) =>
            setState({
                discountList: state.discountList.map(el => {
                    if (el.value === value) {
                        return {...el, isChecked: true};
                    }
        
                    return {...el, isChecked: false};
                })
            })
        }
    />
</Provider>
```
