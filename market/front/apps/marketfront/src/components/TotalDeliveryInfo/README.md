### TotalDeliveryInfo

Отображает блок суммарной информации о доступных доставках.


Дефолтное отображение

```jsx
    import {TotalDeliveryInfo as TotalDeliveryInfoView} from '.';

    const props = {
        courierOption: {
            dayFrom: 6,
            dayTo: 6,
            price: {
                value: 249,
                currency: 'RUB',
            },
        },
        pickupOption: {
            dayFrom: 3,
            dayTo: 4,
            price: {
                value: 0,
                currency: 'RUB',
            },
        },
        postOption: {
            dayFrom: 23,
            dayTo: 24,
            price: {
                value: 120,
                currency: 'RUB',
            },
        },
        dropshipPickupOption: {
            dayFrom: 1,
            dayTo: 2,
            price: {
                value: 100,
                currency: 'RUB',
            },
        },
    };

     <TotalDeliveryInfoView {...props} />
```

Без отображения цены

```jsx
    import {TotalDeliveryInfo as TotalDeliveryInfoView} from '.';

    const props = {
        courierOption: {
            dayFrom: 6,
            dayTo: 6,
            price: {
                value: 249,
                currency: 'RUB',
            },
        },
        pickupOption: {
            dayFrom: 3,
            dayTo: 4,
            price: {
                value: 0,
                currency: 'RUB',
            },
        },
        postOption: {
            dayFrom: 23,
            dayTo: 24,
            price: {
                value: 120,
                currency: 'RUB',
            },
        },
        dropshipPickupOption: {
            dayFrom: 1,
            dayTo: 2,
            price: {
                value: 100,
                currency: 'RUB',
            },
        },
    };

     <TotalDeliveryInfoView {...props} showPrice={false} />
```
