### Песочница

```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground component={OrderTotal} />
</Provider>
```

### Итого заказа

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            deliveryPrice={{value: 200, currency}}
            itemsDiscount={{value: 1000, currency}}
            promocodeDiscount={{value: 200, currency}}
            coinsDiscount={{value: 500, currency}}
            orderPrice={{value: 2500, currency}}
        />
    </div>
</Provider>

```

#### Без скидок

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            deliveryPrice={{value: 200, currency}}
            itemsDiscount={{value: 0, currency}}
            promocodeDiscount={{value: 0, currency}}
            coinsDiscount={{value: 0, currency}}
            orderPrice={{value: 4200, currency}}
        />
    </div>
</Provider>

```


#### C бесплатной бонусной доставкой

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            deliveryPrice={{value: 0, currency}}
            itemsDiscount={{value: 1000, currency}}
            promocodeDiscount={{value: 200, currency}}
            coinsDiscount={{value: 500, currency}}
            orderPrice={{value: 2500, currency}}
            hasDeliveryCoin='true'
        />
    </div>
</Provider>

```

#### C Я.Плюс

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <OrderTotal
        itemsCount='4'
        itemsPrice={{value: 4000, currency}}
        deliveryPrice={{value: 0, currency}}
        itemsDiscount={{value: 1000, currency}}
        promocodeDiscount={{value: 200, currency}}
        coinsDiscount={{value: 500, currency}}
        orderPrice={{value: 2500, currency}}
        hasYandexPlus='true'
    />
</Provider>
```

#### C установленным типом доставки

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            deliveryPrice={{value: 200, currency}}
            itemsDiscount={{value: 1000, currency}}
            promocodeDiscount={{value: 200, currency}}
            coinsDiscount={{value: 500, currency}}
            orderPrice={{value: 2500, currency}}
            deliveryType={'PICKUP'}
        />
    </div>
</Provider>

```

#### C форсированным отображением стоимости доставки

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            itemsDiscount={{value: 1000, currency}}
            promocodeDiscount={{value: 200, currency}}
            coinsDiscount={{value: 500, currency}}
            orderPrice={{value: 2500, currency}}
            deliveryType={'POST'}

            showDelivery={true}
        />
    </div>
</Provider>

```

#### Доступно в кредит

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            itemsDiscount={{value: 1000, currency}}
            orderPrice={{value: 3000, currency}}
            monthlyPayment={{value: 259, currency}}
        />
    </div>
</Provider>

```

#### Недоступно в кредит (мин. сумма)

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            deliveryPrice={{value: 200, currency}}
            orderPrice={{value: 4200, currency}}
            creditNotAvailable={{
                errorType: 'TOO_CHEAP',
                minPrice: {value: 3500, currency}
            }}
        />
    </div>
</Provider>

```

#### Недоступно в кредит (неподходящие товары)

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            deliveryPrice={{value: 200, currency}}
            orderPrice={{value: 4200, currency}}
            creditNotAvailable={{
                errorType: 'CREDIT_NOT_AVAILABLE_FOR_ITEMS',
                itemsCount: 3,
                itemsDescription: 'Нурофен, Ринолайф средство, Фарестон таб. 60 мг',
            }}
        />
    </div>
</Provider>

```

#### В кредит

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <div>
        <OrderTotal
            itemsCount='4'
            itemsPrice={{value: 4000, currency}}
            itemsDiscount={{value: 1000, currency}}
            orderPrice={{value: 3000, currency}}
            isCreditOrder={true}
            monthlyPayment={{value: 259, currency}}
        />
    </div>
</Provider>

```

#### Размер `m`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <OrderTotal
         itemsCount='4'
         itemsPrice={{value: 4000, currency}}
         deliveryPrice={{value: 0, currency}}
         itemsDiscount={{value: 1000, currency}}
         promocodeDiscount={{value: 200, currency}}
         coinsDiscount={{value: 500, currency}}
         orderPrice={{value: 2500, currency}}
         hasDeliveryCoin='true'

        size={'m'}
    />
</Provider>
```

#### Размер `l`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const currency = 'RUB';

<Provider store={store}>
    <OrderTotal
        itemsCount='4'
        itemsPrice={{value: 4000, currency}}
        deliveryPrice={{value: 0, currency}}
        itemsDiscount={{value: 1000, currency}}
        promocodeDiscount={{value: 200, currency}}
        coinsDiscount={{value: 500, currency}}
        orderPrice={{value: 2500, currency}}
        hasDeliveryCoin='true'

        size={'l'}
    />
</Provider>
```
