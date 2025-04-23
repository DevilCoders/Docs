Отвечает за отображение цены и валюты. Принимает объект цены - price/prices.

```jsx
const prices = {
    min: '21050',
    max: '26990',
    currency: 'RUR',
    avg: '24179'
};

<Price price={prices} type="min" />
```

### Параметры

#### type (default - static)

* range - диапазон цен (мин - макс)
* avg - средняя цена
* oldMin - старая цена, используется в блоке скидки
* (static, min, max)

```jsx
const price = {
    currency: "RUR",
    value: "799",
    isDeliveryIncluded: false,
    rawValue: "799",
    discount: {
        oldMin: "2399",
        percent: 67,
        isBestDeal: false
    }
};

<Price price={price} />
```

#### type='credit'

```jsx
const price = {
    currency: "RUR",
    value: "799"
};

<Price price={price} type="credit" />
```

#### Currency

```jsx
const priceKzt = {
    currency: "KZT",
    value: "1799",
    isDeliveryIncluded: false,
    rawValue: "1799",
};

const priceRub = {
    currency: "RUB",
    value: "1799",
    isDeliveryIncluded: false,
    rawValue: "1799",
};

const priceUah = {
    currency: "UAH",
    value: "1799",
    isDeliveryIncluded: false,
    rawValue: "1799",
};

const priceByn = {
    currency: "BYN",
    value: "1799",
    isDeliveryIncluded: false,
    rawValue: "1799",
};

<div style={{fontFamily: 'sans-serif'}}>
    <Price price={priceRub} />
    <br /><br />
    <Price price={priceKzt} />
    <br /><br />
    <Price price={priceUah} />
    <br /><br />
    <Price price={priceByn} />
</div>
```
