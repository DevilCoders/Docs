# HorizontalScroll

Компонент, который можно скроллить в горизонтальной ориентации. Поддерживает touch-листание. Также имеет возможность выходить за пределы родительского блока в стороны, чтобы занять всю ширину экрана.

На время скролла внутри себя блокирует жест закрытия контейнера приложения.

## Пример использования

### Компонент

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';

import { HorizontalScroll } from '@yandex-int/tap-components/HorizontalScroll';
import { ProductCard as ProductCardBase, withSizeS } from '@yandex-int/tap-components/ProductCard';

const ProductCard = compose(withSizeS)(ProductCardBase);

const App: React.FC = () => {
    return (
        <HorizontalScroll>
            <ProductCard
                size="s"
                title="Товар дня"
                image={{ src: 'https://example.com/image-1x-1.png' }}
            />
            <ProductCard
                size="s"
                title="Самый лучший товар"
                image={{ src: 'https://example.com/image-1x-2.png' }}
            />
            <ProductCard
                size="s"
                title="Выгодный товар"
                image={{ src: 'https://example.com/image-1x-3.png' }}
            />
            <ProductCard
                size="s"
                title="Хороший товар"
                image={{ src: 'https://example.com/image-1x-4.png' }}
            />
            <ProductCard
                size="s"
                title="Товар без асбеста"
                image={{ src: 'https://example.com/image-1x-5.png' }}
            />
        </HorizontalScroll>
    );
};
```

### Скелетон

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';

import { HorizontalScrollSkeleton } from '@yandex-int/tap-components/HorizontalScroll';
import { ProductCardSkeleton as ProductCardSkeletonBase, withSkeletonSizeS } from '@yandex-int/tap-components/ProductCard';

const ProductCardSkeleton = compose(withSkeletonSizeS)(ProductCardSkeletonBase);

const ProductCardSkeletonSizeS: React.FC = () => <ProductCardSkeleton size="s" />;

const App: React.FC = () => {
    return <HorizontalScrollSkeleton component={ProductCardSkeletonSizeS} />;
};
```

## Примеры

### Компонент

{{%story:::tap-components-components-horizontalscroll--playground%}}

### Скелетон

{{%story:::tap-components-components-horizontalscroll--skeleton%}}

## Свойства

### Компонент

| Свойство          | Тип                         | Описание                                                                   |
| ----------------- | --------------------------- | -------------------------------------------------------------------------- |
| className?        | `string`                    | Дополнительный класс у корневого DOM-элемента                              |
| contentClassName? | `string`                    | Дополнительный CSS-класс у контейнера с содержимым блока                   |
| innerRef?         | `RefObject<HTMLDivElement>` | Ref-ссылка на контейнер с содержимым блока                                 |
| onError?          | `(err: JSApiError) => void` | Коллбэк ошибки невозможности заблокировать жест закрытия шторки контейнера |

### Скелетон

| Свойство   | Тип                   | Описание                                              |
| ---------- | ---------------- ---- | ------------------------------------------------ ---- |
| className? | `string`              | Дополнительный класс у корневого DOM-элемента         |
| component  | `React.ComponentType` | Компонент, используемый в качестве скелетона элемента |
| count?     | `number`              | Количество скелетонов. По-умолчанию 3                 |

## CSS-переменные

### Компонент

| Переменная                      | Тип  | Описание                                                              |
| ------------------------------- | ---- | --------------------------------------------------------------------- |
| --horizontal-scroll-side-indent | `px` | Величина, на которую нужно "вытащить" блок из родителя слева и справа |

### Скелетон

| Переменная                               | Тип  | Описание                                                              |
| ---------------------------------------- | ---- | --------------------------------------------------------------------- |
| --horizontal-scroll-skeleton-side-indent | `px` | Величина, на которую нужно "вытащить" блок из родителя слева и справа |
