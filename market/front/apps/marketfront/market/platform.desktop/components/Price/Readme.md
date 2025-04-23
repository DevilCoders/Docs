Отвечает за отображение цены и валюты, выводит разные типы цены - credit, promo, avg и т.д. Принимает объект цены - price/prices.

```jsx
import PriceDifferentType from '@self/platform/components/Price'

const prices = {
    min: '21050',
    max: '26990',
    currency: 'RUR',
    avg: '24179'
};

<PriceDifferentType price={prices} type="min" />
```

### Параметры

#### type (default - static)

* range - диапазон цен (мин - макс)
* avg - средняя цена
* oldMin - старая цена, используется в блоке скидки
* (static, min, max)

```jsx
import PriceDifferentType from '@self/platform/components/Price'

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

<PriceDifferentType price={price} />
```

#### type='credit'

```jsx
import PriceDifferentType from '@self/platform/components/Price'

const price = {
    currency: "RUR",
    value: "799"
};

<PriceDifferentType price={price} type="credit" />
```

#### Currency

```jsx
import PriceDifferentType from '@self/platform/components/Price'

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
    <PriceDifferentType price={priceRub} />
    <br /><br />
    <PriceDifferentType price={priceKzt} />
    <br /><br />
    <PriceDifferentType price={priceUah} />
    <br /><br />
    <PriceDifferentType price={priceByn} />
</div>
```
