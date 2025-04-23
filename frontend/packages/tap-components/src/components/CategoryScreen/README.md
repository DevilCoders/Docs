# CategoryScreen

Компонент экрана категории товаров. Позволяет вывести список товаров из данной категории.

В зависимости от переданных свойств компонент может быть отрисован со следующими элементами:

- шапка;
- название бренда, показанного в категории;
- название категории;
- изменение магазина;
- глобальный фильтр;
- список подкатегорий;
- панель фильтрации и сортировки.

## Пример использования

```typescript jsx
import React, { useCallback, useMemo } from 'react';
import { Link, useHistory } from 'react-router-dom';
import { compose } from '@bem-react/core';

import { CategoryScreen } from '@yandex-int/tap-components/CategoryScreen';
import { FilterCurrentValue } from '@yandex-int/tap-components/FilterCurrentValue';
import { FiltersPanel } from '@yandex-int/tap-components/FiltersPanel';
import { HorizontalScroll } from '@yandex-int/tap-components/HorizontalScroll';
import { InfiniteScrollGrid } from '@yandex-int/tap-components/InfiniteScrollGrid';
import {
    ProductCard as ProductCardBase, 
    ProductCardSkeleton as ProductCardSkeletonBase,
    withSizeM,
    withSkeletonSizeM
} from '@yandex-int/tap-components/ProductCard';
import { SearchHeader } from '@yandex-int/tap-components/SearchHeader';
import { SearchInput } from '@yandex-int/tap-components/SearchInput';
import { Text as TextBase, withWeightBold } from '@yandex-lego/components/Text';

const Text = compose(withWeightBold)(TextBase);
const ProductCard = compose(withSizeM)(ProductCardBase);
const ProductCardSkeleton = compose(withSkeletonSizeM)(ProductCardSkeletonBase);

function ProductCardSizeM(props: Omit<React.ComponentProps<typeof ProductCard>, 'size'>) {
    return <ProductCard {...props} size="m" />;
}

const MyCategoryScreen: React.FC = () => {
    const history = useHistory();

    const category = {
        id: '1',
        childCategories: [
            {
                id: '2',
                children: 'Одежда',
                active: true,
                linkComponent: ({ children }) => <Link to="/category/odezhda">{children}</Link>
            },
            {
                id: '3',
                children: 'Обувь',
                active: true,
                linkComponent: ({ children }) => <Link to="/category/obuv">{children}</Link>
            }
        ],
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
        hasMoreItems: true,
        isLoadingMore: false,
        isLoading: false
    };

    const {
        id,
        childCategories,
        items,
        hasMoreItems,
        isLoadingMore,
        isLoading
    } = category;

    const onLoadMore = () => console.log('Loading more!');

    const onGenderClick = useCallback(() => {
        history.push({ pathname: '/filters' });
    }, [history]);

    const sorting = { label: 'По популярности', onClick: () => {} };
    const filter = { count: 0, onClick: () => {} };
    const shopChangerLinkComponent = useMemo(() => {
        const linkComponent: React.FC = ({ children }) => {
            return <Link to={'/shops'}>{children}</Link>;
        };

        return linkComponent;
    }, []);
    const paging = {
        pageSize: 10,
        hasMore: hasMoreItems,
        isLoadingMore,
        onLoadMore,
    };
    const categoryTitle = (
        <Text
            as="h2"
            typography="headline-m"
            weight="bold"
        >
            {category.name}
        </Text>
    );

    return (
        <CategoryScreen
            header={<SearchHeader input={<SearchInput placeholder="Поиск" />} />}
            globalFilters={<div onClick={onGenderClick}>{'Женский'}</div>}
            categoryTitle={categoryTitle}
            categoriesCarousel={(
                <HorizontalScroll>
                    {childCategories.map(childCategory => <Tag key={childCategory.id} {...childCategory} />)}
                </HorizontalScroll>
            )}
            filtersPanel={<FiltersPanel filter={filter} sorting={sorting} />}
            shopChanger={(
                <FilterCurrentValue
                    label="Наличие"
                    linkComponent={shopChangerLinkComponent}
                >
                    2 из 10
                </FilterCurrentValue>
            )}
            products={<InfiniteScrollGrid
                items={items}
                isLoading={isLoading}
                paging={paging}
                component={ProductCardSizeM}
                skeleton={(
                    <>
                        {[...Array(6)].map((_, index) => (<ProductCardSkeleton key={index} size="m" />))}
                    </>
                )}
            />}
        />
    );
};
```

## Пример

{{%story:::tap-components-screens-categoryscreen--playground%}}

## Свойства

| Свойство            | Тип               | Описание                                      | Рекомендуемые компоненты             |
| ------------------- | ----------------- | --------------------------------------------- | ------------------------------------ |
| header?             | `React.ReactNode` | Шапка экрана (например, блок поиска)          | `SearchHeader`, `Header`             |
| globalFilters?      | `React.ReactNode` | Блок глобальных фильтров                      | `TabsMenu`                           |
| brandTitle?         | `React.ReactNode` | Блок выбранного бренда                        | `Text`                               |
| categoryTitle?      | `React.ReactNode` | Блок названия категории                       | `Text`                               |
| categoriesCarousel? | `React.ReactNode` | Блок списка подкатегорий                      | `HorizontalScroll` с `Tag`           |
| filtersPanel?       | `React.ReactNode` | Блок сортировки и фильтрации                  | `FiltersPanel`                       |
| shopChanger?        | `React.ReactNode` | Блок выбора магазина                          | `FilterCurrentValue`                 |
| products            | `React.ReactNode` | Блок списка товаров                           | `InfiniteScrollGrid` с `ProductCard` |
| className?          | `string`          | Дополнительный класс у корневого DOM-элемента |                                      |

## CSS-переменные

| Переменная                     | Тип          | Описание                                            |
| ------------------------------ | ------------ | --------------------------------------------------- |
| --category-screen-bg-color     | `color`      | Цвет фона экрана                                    |
| --category-screen-header-align | `text-align` | Выравнивание в заголовках экрана и фильтре магазина |
| --category-screen-side-padding | `px`         | Отступ экрана от края экрана слева и справа         |
