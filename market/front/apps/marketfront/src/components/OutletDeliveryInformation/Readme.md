Отображает сводную информацию о доставке в пункте выдачи заказа.

```jsx
    
const schedule = [{
    days: {
        from: 1,
        to: 5,
    },
    time: {
        from: '10:00',
        to: '21:00',
    },
}];

const dates = {
    fromDate: '03-12-2018',
    toDate: '03-12-2018',
};

const address = {
    fullAddress: 'Москва, пр. 1-й Магистральный, д. 12, стр.1',
}

const price = {
    value: 150,
    currency: 'RUB'
};

<OutletDeliveryInformation
    name={'Пункт выдачи посылок PickPoint'}
    address={address}
    schedule={schedule}
    dates={dates}
    price={price}
/>
   
```
