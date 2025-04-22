# OrderInfo

Компонент информации о заказе. 

С его помощью можно:

- Вывести описание заказа.
- Показать картинки товаров.
- Показать лейбл состояния заказа.

## Пример использования

### Компонент

```typescript jsx
import React from 'react';
import { Link } from 'react-router-dom';
import { Label } from '@yandex-int/tap-components/Label';
import { OrderInfo } from '@yandex-int/tap-components/OrderInfo';

const linkComponent: React.FC = ({ children }) => (<Link to="/krossovki">{children}</Link>);

const products = [
    {
        image: { src: 'image1-1x.png', src2x: 'image1-2x.png' },
        title: 'Кроссовки',
        linkComponent
    },
    { image: { src: 'image2-1x.png', src2x: 'image2-2x.png' }, title: 'Носки' },
    { image: { src: 'image3-1x.png', src2x: 'image3-2x.png' }, title: 'Зонт' },
];
const description = (
    <>
        <b>Отложить вещи в ТЦ Global Mall</b><br />
        <span>Ленинградское шоссе, 16А, стр. 4<br />Срок хранения заказа: 2 дня</span>
    </>
);

const App: React.FC = () => {
    return  (
        <OrderInfo
            className="my-order"
            header="Заказ №390958"
            label={<Label>Оплачен</Label>}
            products={products}
            description={description}
        />
    );
};
```

### Скелетон

```typescript jsx
import React from 'react';
import { OrderInfoSkeleton } from '@yandex-int/tap-components/OrderInfo';

const App: React.FC = () => {
    return <OrderInfoSkeleton className="my-order" />;
};
```

## Примеры

### Компонент

{{%story:::tap-components-e-commerce-orderinfo--playground%}}

### Скелетон

{{%story:::tap-components-e-commerce-orderinfo--skeleton%}}

## Свойства

| Свойство     | Тип                  | Описание                                      |
| ------------ | -------------------- | --------------------------------------------- |
| className?   | `string`             | Дополнительный класс у корневого DOM-элемента |
| description? | `ReactNode`          | Дополнительное описание заказа                |
| header       | `ReactNode`          | Заголовок карточки заказа                     |
| label?       | `ReactNode`          | Лейбл карточки заказа                         |
| products     | `Array<ProductItem>` | Информация о товарах в заказе                 |

```typescript jsx
type ProductItem = {
    title: string;
    image?: {
        src: string;
        src2x?: string;
    };
    linkComponent?: React.ComponentType; // Компонент для оборачивания товара в ссылку
};
```

## CSS-переменные

| Переменная                      | Тип     | Описание                            |
| ------------------------------- | ------- | ----------------------------------- |
| --order-info-product-height     | `px`    | Высота изображения товара           |
| --order-info-product-width      | `px`    | Ширина изображения товара           |
| --order-info-header-color       | `color` | Цвет заголовка карточки товара      |
| --order-info-header-margin      | `px`    | Отступ от заголовка карточки товара |
| --order-info-description-color  | `color` | Цвет дополнительного описания       |
| --order-info-description-margin | `px`    | Отступ от описания до картинок      |
