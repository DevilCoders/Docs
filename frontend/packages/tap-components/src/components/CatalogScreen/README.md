# CatalogScreen

Страница каталога товаров.

Позволяет вывести:

- карусель брендов;
- блок фильтра;
- строку поиска;
- список категорий.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { Link } from 'react-router-dom';
import { compose } from '@bem-react/core'
import { CatalogScreen } from '@yandex-int/tap-components/CatalogScreen';
import { CategoryList } from '@yandex-int/tap-components/CategoryList';
import { EntityCarousel } from '@yandex-int/tap-components/EntityCarousel';
import { SearchHeader } from '@yandex-int/tap-components/SearchHeader';
import { SearchInput } from '@yandex-int/tap-components/SearchInput';
import { TabsMenu as TabsMenuBase, withSizeM, withLayoutHoriz, withViewDefault } from '@yandex-int/tap-components/TabsMenu'

const TabsMenu = compose(
    withSizeM,
    withViewDefault,
    withLayoutHoriz,
)(TabsMenuBase);

const MyCatalogScreen: React.FC = () => {
    const [activeTab, setActiveTab] = useState('male');
    const brands = [
        {
            id: 1,
            name: 'Adidas',
            image: { src: '/images/adidas' },
            linkComponent: ({ children }) => <Link to="/brand/adidas">{children}</Link>
        },
        {
            id: 2,
            name: 'Puma',
            image: { src: '/images/puma' },
            linkComponent: ({ children }) => <Link to="/category/puma">{children}</Link>
        },
    ];
    const categories = [
        {
            id: 1,
            name: 'Одежда',
            image: { src: '/images/odezhda' },
            linkComponent: ({ children }) => <Link to="/category/odezhda">{children}</Link>
        },
        {
            id: 2,
            name: 'Обувь',
            image: { src: '/images/obuv' },
            linkComponent: ({ children }) => <Link to="/category/obuv">{children}</Link>
        },
    ];

    return (
        <CatalogScreen
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
            brands={<EntityCarousel
                entities={brands}
                title="Бренды"
            />}
            categories={<CategoryList categories={categories} />}
        />
    );
};
```

## Пример

{{%story:::tap-components-screens-catalogscreen--playground%}}

## Свойства

| Свойство       | Тип               | Описание                                      | Рекомендуемые компоненты |
| -------------- | ----------------- | --------------------------------------------- | ------------------------ |
| header?        | `React.ReactNode` | Шапка экрана (например, блок поиска)          | `SearchHeader`, `Header` |
| globalFilters? | `React.ReactNode` | Блок глобальных фильтров                      | `TabsMenu`               |
| brands?        | `React.ReactNode` | Блок карусели брендов                         | `EntityCarousel`         |
| categories     | `React.ReactNode` | Блок списка подкатегорий                      | `CategoryList`           |
| className?     | `string`          | Дополнительный класс у корневого DOM-элемента |                          |

## CSS-переменные

| Переменная                    | Тип     | Описание                                      |
| ----------------------------- | ------- | --------------------------------------------- |
| --catalog-screen-bg-color     | `color` | Цвет фона экрана                              |
| --catalog-screen-main-accent  | `color` | Акцентный цвет экрана                         |
| --catalog-screen-side-padding | `px`    | Отступ страницы от края экрана слева и справа |
