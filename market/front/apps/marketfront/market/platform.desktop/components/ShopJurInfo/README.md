# ShopJurInfo

Компонент отображения юридической информации о магазине.

## Примеры использования

### Пример 1. Все данные в наличии
```jsx
const ShopJurInfo = require('@self/platform/components/ShopJurInfo').default;
const shopInfo = require('./__fixtures__/shopJurInfo.json');

<ShopJurInfo shopId={shopInfo.id} shopInfo={shopInfo} />
```

### Пример 2. Нет данных о названии магазина
```jsx
const ShopJurInfo = require('@self/platform/components/ShopJurInfo').default;
const shopInfo = Object.assign(
    {},
    require('./__fixtures__/shopJurInfo.json'),
    {
        shopName: undefined,
        name: undefined,
        shopBrandName: undefined,
        brandName: undefined,
    }
);

<ShopJurInfo shopId={shopInfo.id} shopInfo={shopInfo} />
```

### Пример 2. Нет юридической информации о магазине
```jsx
const ShopJurInfo = require('@self/platform/components/ShopJurInfo').default;
const shopInfo = require('./__fixtures__/shopJurInfo.json');

<ShopJurInfo shopId={shopInfo.id} shopInfo={undefined} />
```

### Пример 3. Несколько блоков друг за другом
```jsx
const ShopJurInfo = require('@self/platform/components/ShopJurInfo').default;
const shopInfo = require('./__fixtures__/shopJurInfo.json');

<div>
    <ShopJurInfo shopId={shopInfo.shopId} shopInfo={shopInfo} />
    <ShopJurInfo shopId={shopInfo.shopId} shopInfo={shopInfo} />
    <ShopJurInfo shopId={shopInfo.shopId} shopInfo={undefined} />
    <ShopJurInfo shopId={shopInfo.shopId} shopInfo={shopInfo} />
</div>
```
