# ProductsSection

Компонент секции товаров.

В зависимости от переданных свойств компонент может быть отрисован со следующими элементами:

- заголовок секции;
- теги, например, карусель тегов;
- товары, например, карусели товаров.

## Пример использования

```typescript jsx
import React from 'react';
import { Link } from 'react-router-dom';
import { compose } from '@bem-react/core';

import { HorizontalScroll } from '@yandex-int/tap-components/HorizontalScroll';
import {
    ProductCard as ProductCardBase,
    withSizeS
} from '@yandex-int/tap-components/ProductCard';
import { ProductsSection } from '@yandex-int/tap-components/ProductsSection';
import { SectionHeader } from '@yandex-int/tap-components/SectionHeader';
import { Tag, TagProps } from '@yandex-int/tap-components/Tag';

const ProductCard = compose(withSizeS)(ProductCardBase);

const App: React.FC = () => {
    const tags: Array<TagProps> = [
        { id: '1', children: 'Кроссовки' },
        { id: '2', children: 'Ботинки', active: true },
        { id: '3', children: 'Туфли' }
    ];
    const products = [
        {
            id: '1',
            title: 'Осенние ботинки',
            image: { src: '/images/product/1' },
            price: {
                current: '1 000 ₽',
                old: '2 000 ₽',
            },
        },
        {
            id: '2',
            title: 'Летние ботинки',
            image: { src: '/images/product/2' },
            price: {
                current: '1 200 ₽',
                old: '2 400 ₽',
            },
        }
    ];
    const saleLinkComponent: React.FC = ({ children }) => (<Link to="/sale">{children}</Link>);

    return (
        <ProductsSection
            header={(
                <SectionHeader
                    title="Распродажа"
                    linkComponent={saleLinkComponent}
                    linkText="Смотреть все"
                />
            )}
            tags={(
                  <HorizontalScroll>
                      {tags.map(tag => <Tag key={tag.id} {...tag} />)}
                  <HorizontalScroll />
              )}
            products={(
                  <HorizontalScroll>
                      {products.map(prouduct => <ProductCard key={prouduct.id} size="s" {...prouduct} />)}
                  <HorizontalScroll />
              )}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-productssection--playground%}}

## Свойства

| Свойство   | Тип               | Описание                                      | Рекомендуемые компоненты                                    |
| ---------- | ----------------- | --------------------------------------------- | ----------------------------------------------------------- |
| className? | `string`          | Дополнительный класс у корневого DOM-элемента |                                                             |
| header?    | `React.ReactNode` | Блок заголовка                                | `SectionHeader`                                             |
| products   | `React.ReactNode` | Блок товаров                                  | `HorizontalScroll` или `InfiniteScrollGrid` с `ProductCard` |
| tags?      | `React.ReactNode` | Блок тегов                                    | `HorizontalScroll` с `Tag`                                  |

## CSS-переменные

| Переменная                       | Тип  | Описание                     |
| -------------------------------- | ---- | ---------------------------- |
| --products-section-header-margin | `px` | Отступ после названия блока  |
| --products-section-tags-margin   | `px` | Отступ после блока категорий |
