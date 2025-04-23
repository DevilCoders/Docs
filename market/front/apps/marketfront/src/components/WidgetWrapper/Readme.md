### Обертка над виджетом

#### На примере информации о доставке
```jsx noeditor
    import {TotalDeliveryInfo} from '@self/root/src/components/TotalDeliveryInfo';

    const deliveryInfoProps = {
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

<Helper.Playground
    component={WidgetWrapper}
    forceUpdate={true}
    example={props => (
        <WidgetWrapper {...props}>
            <TotalDeliveryInfo {...deliveryInfoProps} />
        </WidgetWrapper>
    )}
    settings={{background: 'transparent'}}
    defaultValues={{
        background: {
            color: '$white'
        },
        paddings: {
            top: '5',
            bottom: '5',
            left: '5',
            right: '5'
        },
        borders: {
            top: true,
            bottom: true,
            color: '$gray400'
        },
        font: {
            size: '250',
        },
        title: {
            text: 'Информация о доставке',
            indent: '5'
        },
        closer: {
            closable: true,
        }
    }}
/>
```
