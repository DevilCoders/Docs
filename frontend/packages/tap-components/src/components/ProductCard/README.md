# ProductCard

Карточка товара, предназначенная для использования в списках и слайдерах.

## Пример использования

### Компонент с необходимым набором свойств

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { ProductCard as ProductCardBase, withSizeS } from '@yandex-int/tap-components/ProductCard';

const ProductCard = compose(withSizeS)(ProductCardBase);

const App: React.FC = () => {
    return (
        <ProductCard
            title="Товар дня"
            image={{ src: 'https://example.com/image-1x.png' }}
        />
    );
};
```

### Компонент с полным набором свойств

```typescript jsx
import React from 'react';
import { ProductCard, Currency } from '@yandex-int/tap-components/ProductCard';

const App: React.FC = () => {
    return (
        <ProductCard
            size="s"
            title="Товар дня"
            description="выбор покупателей"
            image={{ src: 'https://example.com/image-1x.png', width: 124, height: 172 }}
            image2x={{ src: 'https://example.com/image-2x.png', width: 248, height: 344 }}
            price={{
                current: { from: 1000 * 100, to: 1200 * 100 },
                old: 2000 * 100,
                currency: Currency.RUB
            }}
            button={{
                text: 'Добавить в корзину',
                onClick: () => console.log('Clicked on Button!')
            }}
            discount="-35%"
            url="/product/123"
            onClick={() => console.log('Clicked!')}
            className="my-product-card"
        />
    );
};
```

### Скелетон

```typescript jsx
import React from 'react';
import { composeU } from '@bem-react/core';
import {
    ProductCardSkeleton as ProductCardSkeletonBase,
    withSkeletonSizeS,
    withSkeletonSizeM
} from '@yandex-int/tap-components/ProductCard';

const ProductCardSkeleton = composeU(withSkeletonSizeS, withSkeletonSizeM)(ProductCardSkeletonBase);

const App: React.FC = () => {
    return <ProductCardSkeleton className="my-product-card" size="s" />;
};
```

## Примеры

### Компонент

{{%story:::tap-components-e-commerce-productcard--playground%}}

### Размеры

{{%story:::tap-components-e-commerce-productcard--sizes%}}

### Скелетон

{{%story:::tap-components-e-commerce-productcard--skeleton%}}

## Свойства

| Свойство       | Тип                                                                     | Описание                                                                     |
| -------------- | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| button?        | `{ text: string; onClick?: (event: MouseEvent<HTMLElement>) => void; }` | Настройки кнопки                                                             |
| className?     | `string`                                                                | Дополнительный класс у корневого DOM-элемента                                |
| description?   | `ReactNode`                                                             | Описание товара                                                              |
| discount?      | `string`                                                                | Текст со скидкой                                                             |
| image          | `{ src: string; width?: number; height?: number }`                      | Картинка товара                                                              |
| image2x?       | `{ src: string; width?: number; height?: number }`                      | Картинка для экранов с высокой плотностью пикселей                           |
| linkComponent? | `React.ComponentType`                                                   | Компонент, оборачивающий `children` в ссылку; делает элемент целиком ссылкой |
| noImageNode?   | `ReactNode`                                                             | Заглушка для отсутствующего изображения                                      |
| noImageText?   | `string`                                                                | Текст для надписи об отсутствии фото                                         |
| onClick?       | `(event: MouseEvent<HTMLElement>) => void`                              | Обработчик, который вызывается при нажатии на карточку                       |
| price?         | `{ current: React.ReactNode; old?: React.ReactNode; }`                  | Цена товара                                                                  |
| size?          | `Size`                                                                  | Размер карточки                                                              |
| title          | `string`                                                                | Название товара                                                              |

```typescript jsx
type Size = 's' | 'm';

type Price = {
    current: number | { from?: number; to?: number; };
    old?: number | null;
    currency?: Currency;
};
```

## CSS-переменные

| Переменная               | Тип      | Описание                                                      |
| ------------------------ | -------- | ------------------------------------------------------------- |
| --product-card-bg-color  | `color`  | Цвет фона в карточке                                          |
| --product-card-color     | `color`  | Цвет текста в карточке                                        |
| --product-card-img-ratio | `number` | Соотношение сторон картинки в карточке (только для размера М) |
