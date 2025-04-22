# MainScreen

Компонент главной страницы магазина.

Позволяет вывести логотип, блок фильтра, строку поиска, а также набор каруселей товаров, баннеров и списков товаров, расположенных по заданному лейауту.

В зависимости от переданных свойств компонент главной страницы может быть отрисован со следующими элементами:

- логотип;
- глобальные фильтры;
- поиск;
- карусель товаров;
- баннеры;
- список товаров.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { Link } from 'react-router-dom';
import { compose, composeU } from '@bem-react/core';

import { HorizontalScroll } from '@yandex-int/tap-components/HorizontalScroll';
import {
    MessageBox as MessageBoxBase,
    withSizeM,
    withViewDefault,
    Wrapper
} from '@yandex-int/tap-components/MessageBox';
import { MainScreen } from '@yandex-int/tap-components/MainScreen';
import { InfiniteScrollGrid } from '@yandex-int/tap-components/InfiniteScrollGrid';
import {
    ProductCard as ProductCardBase,
    ProductCardSkeleton as ProductCardSkeletonBase,
    withSizeS,
    withSizeM,
    withSkeletonSizeM
} from '@yandex-int/tap-components/ProductCard';
import { ProductsSection } from '@yandex-int/tap-components/ProductsSection';
import { SearchHeader } from '@yandex-int/tap-components/SearchHeader';
import { SearchInput } from '@yandex-int/tap-components/SearchInput';
import { SectionHeader } from '@yandex-int/tap-components/SectionHeader';
import { TabsMenu as TabsMenuBase, withSizeM, withLayoutHoriz, withViewDefault } from '@yandex-int/tap-components/TabsMenu'
import { Tag } from '@yandex-int/tap-components/Tag';

const ProductCard = composeU(withSizeS, withSizeM)(ProductCardBase);
const ProductCardSkeleton = compose(withSkeletonSizeM)(ProductCardSkeletonBase);
const MessageBox = compose(withSizeM, withViewDefault)(MessageBoxBase);
const TabsMenu = compose(
    withSizeM,
    withViewDefault,
    withLayoutHoriz,
)(TabsMenuBase);

function ProductCardSizeM(props: Omit<React.ComponentProps<typeof ProductCard>, 'size'>) {
    return <ProductCard {...props} size="m" />;
}

const MyMainScreen: React.FC = () => {
    const [activeTab, setActiveTab] = useState('male');
    const products = [
        {
            id: '1',
            image: {
                src: '/images/1',
            },
            discount: '-50%',
            price: {
                current: '1 000 ₽',
                old: '2 000 ₽',
            },
            title: 'Ремень ручной работы',
            description: 'Ремни',
        },
        {
            id: '2',
            image: {
                src: '/images/2',
            },
            discount: '-50%',
            price: {
                current: '2 000 ₽',
                old: '4 000 ₽',
            },
            title: 'Ремень из натуральной кожи',
            description: 'Ремни',
        }
    ];
    const categories = [
        { id: '', children: 'Все' },
        { id: '1', children: 'Ремни', active: true },
        { id: '2', children: 'Кроссовки' },
        { id: '3', children: 'Ботинки' },
        { id: '4', children: 'Балетки' },
    ];
    const recommendedProducts = {
        items: [
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
        ],
        isLoading: false,
        paging: {
            pageSize: 10,
            hasMore: true,
            isLoadingMore: false,
            onLoadMore: () => console.log('Loading more!'),
        }
    };
    const saleLinkComponent: React.FC = ({ children }) => (<Link to="/sale">{children}</Link>);

    return (
        <MainScreen
            logo={<div>Логотип</div>}
            header={<SearchHeader input={<SearchInput placeholder="Поиск" />} />}
            globalFilters={<TabsMenu
                size="m"
                view="default"
                layout="horiz"
                activeTab={activeTab}
                tabs={[
                    { id: 'male', onClick: () => setActiveTab('male'), content: 'Мужчинам' },
                    { id: 'female', onClick: () => setActiveTab('female'), content: 'Женщинам' },
                ]}
            />}
            layout={[
                <ProductsSection
                    header={<SectionHeader title="Новинки" />}
                    tags={(
                        <HorizontalScroll>
                            {categories.map(category => <Tag key={category.id} {...category} />)}
                        </HorizontalScroll>
                    )}
                    products={(
                        <HorizontalScroll>
                            {products.map(product => <ProductCard key={product.id} size="s" {...product} />)}
                        </HorizontalScroll>
                    )}
                />,
                <MessageBox view="default" size="m">
                    <Wrapper>
                        <h3>Отложить в магазине</h3>
                        <ul>
                            <li>Полностью бесплатно</li>
                            <li>В магазине товар можно примерить</li>
                            <li>Можно купить только то, что подошло</li>
                        </ul>
                    </Wrapper>
                </MessageBox>,
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
                            {categories.map(category => <Tag key={category.id} {...category} />)}
                        </HorizontalScroll>
                    )}
                    products={(
                        <HorizontalScroll>
                            {products.map(product => <ProductCard key={product.id} size="s" {...product} />)}
                        </HorizontalScroll>
                    )}
                />,
                <ProductsSection
                    header={<SectionHeader title="Рекомендуем" />}
                    products={(
                        <InfiniteScrollGrid
                            items={recommendedProducts.items}
                            isLoading={recommendedProducts.isLoading}
                            paging={recommendedProducts.paging}
                            component={ProductCardSizeM}
                            skeleton={(
                                <>
                                    {[...Array(6)].map((_, index) => (<ProductCardSkeleton key={index} size="m" />))}
                                </>
                            )}
                        />
                    )}
                />,
            ]}
        />
    );
};
```

## Пример

{{%story:::tap-components-screens-mainscreen--playground%}}

## Свойства

| Свойство       | Тип                      | Описание                                      | Рекомендуемые компоненты        |
| -------------- | ------------------------ | --------------------------------------------- | ------------------------------- |
| logo?          | `React.ReactNode`        | Блок логотипа                                 |                                 |
| header?        | `React.ReactNode`        | Блок шапки                                    | `Search`, `Header`              |
| globalFilters? | `React.ReactNode`        | Блок глобальных фильтров                      | `TabsMenu`                      |
| layout         | `Array<React.ReactNode>` | Массив блоков основного лейаута               | `ProductsSection`, `MessageBox` |
| className?     | `string`                 | Дополнительный класс у корневого DOM-элемента |                                 |


## CSS-переменные

| Переменная                       | Тип       | Описание                               |
| -------------------------------- | --------- | -------------------------------------- |
| --main-screen-bg-color           | `color`   | Цвет фона экрана                       |
| --main-screen-top-padding        | `px`      | Отступ от края экрана сверху           |
| --main-screen-side-padding       | `px`      | Отступ от края экрана слева и справа   |
| --main-screen-bottom-padding     | `px`      | Отступ от края экрана снизу            |
| --main-screen-layout-item-margin | `px`      | Расстояние между блоками лейаута       |
| --main-screen-logo-z-index       | `z-index` | Слой, на котором располагается логотип |
