# ShopSelect

Компонент выбора магазина из списка. Магазины отображаются как карусель `OrderInfo` с миниатюрами товаров, которые есть в этих магазинах. Если выбран магазин, то отображается только он и кнопка изменения выбора.

 вывести:

- список магазинов для выбранных товаров;
- один из магазинов списка и сбросить выбор;
- выбранный магазин.

## Пример использования

```typescript jsx
import React, { useState } from 'react';

import { ShopSelect } from '@yandex-int/tap-components/ShopSelect';

const App: React.FC = () => {
    const shopsWithProducts = [
        {
            shop: {
                id: '1',
                name: 'ТРК Авиапарк',
                address: 'Ленинградское шоссе, 16А, стр. 4'
            },
            products: [
                { image: { src: 'image1-1x.png', src2x: 'image1-2x.png' }, title: 'Кроссовки' },
                { image: { src: 'image2-1x.png', src2x: 'image2-2x.png' }, title: 'Носки' },
                { image: { src: 'image3-1x.png', src2x: 'image3-2x.png' }, title: 'Зонт' },
            ]
        },
        {
            shop: {
                id: '2',
                name: 'ТЦ Аврора Плаза',
                address: 'ул. Льва Толстого, 16'
            },
            products: [
                { image: { src: 'image1-1x.png', src2x: 'image1-2x.png' }, title: 'Кроссовки' },
                { image: { src: 'image2-1x.png', src2x: 'image2-2x.png' }, title: 'Носки' },
            ]
        }
    ];

    const [selectedShopId, setSelectedShopId] = useState<string | number | null>(null);

    return (
        <ShopSelect
            shopsWithProducts={shopsWithProducts}
            selectedShopId={selectedShopId}
            totalItemsCount={3}
            onShopSelect={setSelectedShopId}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-shopselect--playground%}}

## Свойства

| Свойство           | Тип                       | Описание                                                             |
| ------------------ | ------------------------- | -------------------------------------------------------------------- |
| className?         | `string`                  | Дополнительный класс у корневого DOM-элемента                        |
| onShopSelect       | `(id: ID | null) => void` | Обработчик выбора магазина и сброса выбора                           |
| selectedShopId?    | `ID | null`               | Идентификатор выбранного магазина или `null`, если магазин не выбран |
| shopsWithProducts? | `Array<ShopWithProducts>` | Информация о магазинах и товарах в них                               |

```typescript jsx
import { OrderInfoProductItem } from '@yandex-int/tap-components/OrderInfo';

type ID = string | number;

type Shop = {
    id: ID;             // Используется для ключей массива и обработчика выбора
    name: string;       // Название магазина
    address?: string;   // Адрес магазина
    distance?: string;  // Расстояние до магазина, например, «1,5 км»
};

type ShopWithProducts = {
    shop: Shop; 							// Информация о магазине
    products: Array<OrderInfoProductItem>; 	// Информация о продуктах
    properties?: React.ReactNode; 			// Дополнительные свойства,
                                            // например, текст «Срок хранения заказа: 2 дня» или «5 из 5 в наличии»
};
```
