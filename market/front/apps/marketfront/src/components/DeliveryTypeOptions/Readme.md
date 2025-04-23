## Overview

Компонент выбора способа получения.

### Примеры

##### Есть опции
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => {});

const props = {
    optionsCount: 10,
    cartId: 'cartId_1',
    cartGroupId: 'cartGroupId_1',
};

initialState = {
    currentType: 'DELIVERY',
};

const onOptionClick = currentType => {
    setState({
        currentType,
    });
};

<Provider store={store}>
    <DeliveryTypeOptions
        optionsCount={10}
        cartId='cartId_1'
        cartGroupId='cartGroupId_1'
        availableDeliveryTypes={{
            DELIVERY: [{}],
            PICKUP: [{outlets: [111, 222]}],
            POST: [{}],
        }}
        onChange={onOptionClick}
        currentType={state.currentType}
    />
</Provider>
```

##### Пустые опции
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => {});

<Provider store={store}>
    <DeliveryTypeOptions
        optionsCount={10}
        cartId='cartId_1'
        cartGroupId='cartGroupId_1'
        availableDeliveryTypes={{
            DELIVERY: [],
            PICKUP: [],
            POST: [],
        }}
        currentType={''}
    />
</Provider>
```

##### Отсутствуют опции
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => {});

<Provider store={store}>
    <DeliveryTypeOptions availableDeliveryTypes={{}} />
</Provider>
```
