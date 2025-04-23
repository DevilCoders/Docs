# CartProductItem

Компонент для отображения товара в корзине. Позволяет:

- Вывести иконку контекстного действия с товаров, если передан `callback`.
- Вывести лейбл товара.
- Вывести поле скидки с произвольным текстом.
- Отобразить название и количество товара.
- Отобразить дополнительные свойства товара.
- Отобразить старую и новую цену.
- Вывести кнопку, если передан `button`.

## Пример использования

### Компонент

```typescript jsx
import React from 'react';
import { CartProductItem } from '@yandex-int/tap-components/CartProductItem';

const onContextMenuClick = e => {
    console.info('Triggered context menu for product');
};

const App: React.FC = () => {
    const product = {
        id: 'id1',
        title: 'Teapot',
        image: { src: 'image1-1x.png' },
        properties: ['количество: 1 шт', 'размер: 27']
    };

    return  (
        <CartProductItem
            className="product"
            product={product}
            onContextMenuClick={onContextMenuClick}
        />
    );
};
```

### Скелетон

```typescript jsx
import React from 'react';
import { CartProductItemSkeleton } from '@yandex-int/tap-components/CartProductItem';

const App: React.FC = () => {
    return <CartProductItemSkeleton />;
};
```

## Примеры

### Компонент

{{%story:::tap-components-e-commerce-cartproductitem--playground%}}

### Скелетон

{{%story:::tap-components-e-commerce-cartproductitem--skeleton%}}

## Свойства

| Свойство            | Тип                                        | Описание                                      |
| ------------------- | ------------------------------------------ | --------------------------------------------- |
| button?             | `CartProductItemButton`                    | Настройки кнопки                              |
| className?          | `string`                                   | Дополнительный класс у корневого DOM-элемента |
| onContextMenuClick? | `(event: MouseEvent<HTMLElement>) => void` | Обработчик для контекстного меню товара       |
| product             | `CartProductItemType`                      | Объект товара в корзине                       |

```typescript jsx
type CartProductItemType = {
    title: string;
    image?: {
        src: string;
        width?: number;
        height?: number;
    };
    image2x?: {
        src: string;
        width?: number;
        height?: number;
    };
    label?: React.Node; // Лейбл карточки товара
    discount?: string; // Текст на поле скидки на картинке
    properties?: Array<React.ReactNode>;
    price?: {
        current: React.ReactNode;
        old?: React.ReactNode;
    };
    linkComponent?: React.ComponentType; // Компонент для оборачивания товара в ссылку
};

type CartProductItemButton = {
    text: string;
    onClick?: (event: React.MouseEvent<HTMLElement>) => void;
};
```

## CSS-переменные

| Переменная                              | Тип     | Описание                           |
| --------------------------------------- | ------- | ---------------------------------- |
| --cart-product-item-image-height        | `px`    | Высота картинки                    |
| --cart-product-item-image-width         | `px`    | Ширина картинки                    |
| --cart-product-item-image-border-radius | `px`    | Радиус скругления картинки         |
| --cart-product-item-image-bg-color      | `color` | Цвет заглушки картинки             |
| --cart-product-item-title-color         | `color` | Цвет названия товара               |
| --cart-product-item-properties-color    | `color` | Цвет дополнительных свойств товара |
