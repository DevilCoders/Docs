## Overview

Компонент выбора способа оплаты.

## Props

```jsx static

// Пример не работает в стайлгайдисте из-за неправильного резолва `createPlatformProxyComponent`
// Импорт объекта превращается в функцию (props) => {}

const {PAYMENT_METHOD} = require('@self/root/src/entities/payment');

const options = [
    {method: 'CASH_ON_DELIVERY', title: 'При получении', description: 'Наличными'},
    {method: 'CARD_ON_DELIVERY', title: 'При получении', description: 'Картой'},
    {method: 'YANDEX', title: 'Оплата онлайн', description: 'Банковской картой'},
];

initialState = {
    value: {method: 'CASH_ON_DELIVERY', title: 'При получении', description: 'Наличными'},
};

const onOptionClick = (option) => {
    setState({
        value: option,
    });
};

<PaymentOptions
    activeOption={state.value}
    options={options}
    onOptionClick={onOptionClick}
/>
```
