# InfiniteScrollGrid

Компонент подгружаемого списка. 

Позволяет вывести список любых элементов в виде бесконечной подгружаемой ленты. Лента может быть кастомизирована вставками других элементов через передачу параметра `additionals`.

Элементы рендерятся с данными, переданными в `items`, с помощью компонента, переданного в `component`.

## Пример использования

```typescript jsx
import React from 'react';
import { ProductCard, ProductCardSkeleton } from '@yandex-int/tap-components/ProductCard';
import { InfiniteScrollGrid } from '@yandex-int/tap-components/InfiniteScrollGrid';

const MyInfiniteScrollGrid: React.FC = () => {
    const items = [
        {
            title: 'Куртка мужская',
            image: { src: '/images/1' }
        },
        {
            title: 'Кроссовки женские',
            image: { src: '/images/2' }
        },
        {
            title: 'Куртка женская',
            image: { src: '/images/3' }
        },
        {
            title: 'Кроссовки мужские',
            image: { src: '/images/4' }
        }
    ];
    const hasMoreItems = true;
    const isLoadingMore = false;
    const isLoading = false;

    const onLoadMore = () => console.log('Loading more!');

    const paging = {
        pageSize: 10,
        hasMore: hasMoreItems,
        isLoadingMore,
        onLoadMore,
    };

    return (
        <InfiniteScrollGrid
            items={items}
            isLoading={isLoading}
            paging={paging}
            component={ProductCard}
            skeleton={(
                <>
                    {[...Array(6)].map((_, i) => (<ProductCardSkeleton key={i} />))}
                </>
            )}
        />
    );
};
```

## Пример

{{%story:::tap-components-components-infinitescrolllist--playground%}}

## Свойства

```typescript
type InfiniteScrollGridAdditional = {
    order: number; // Позиция элемента изначального списка, перед которым будет вставлен дополнительный элемент
    children: React.ReactNode; // Элемент вставки
};

type InfiniteScrollGridPaging = {
    pageSize: number;
    hasMore: boolean;
    isLoadingMore: boolean; // Флаг, идет ли сейчас подгрузка
    onLoadMore: () => void; // Обработчик  для загрузки следующих элементов, когда все предыдущие пролистаны до конца
};

type InfiniteScrollGridProps<Item> = {
    items: Array<Item>;
    component: React.ComponentType<Item>; // Компонент рендеринга карточки элемента
    paging?: InfiniteScrollGridPaging;
    isLoading?: boolean; // Флаг индикации загрузки первоначального списка
    skeleton?: React.ReactNode;
    additionals?: Array<InfiniteScrollGridAdditional>;
    // Если в additionals будет несколько элементов с одинаковым order, то будет взят последний
    className?: string;
};
```

| Свойство     | Тип                                   | Описание                                      |
| ------------ | ------------------------------------- | --------------------------------------------- |
| additionals? | `Array<InfiniteScrollGridAdditional>` | Элементы дополнительной вставки в список      |
| className?   | `string`                              | Дополнительный класс у корневого DOM-элемента |
| component    | `React.ComponentType<Item>`           | Компонент-рендерер карточки элемента          |
| isLoading?   | `boolean`                             | Флаг, идет ли загрузка элементов              |
| items        | `Array<Item>`                         | Информация об элементах в списке              |
| paging?      | `InfiniteScrollGridPaging`            | Пагинация списка                              |
| skeleton?    | `React.ReactNode`                     | Скелетон списка карточек                      |

## Поддержка

Для работы в старых версиях браузера необходим [полифил](https://github.com/w3c/IntersectionObserver/tree/master/polyfill) для `IntersectionObserver`

Поддержка без полифила:

Safari >= 11 \
Chrome >= 52
