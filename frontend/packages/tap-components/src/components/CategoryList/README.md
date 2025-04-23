# CategoryList

Список категорий.

## Пример использования

```typescript jsx
import React from 'react';
import { CategoryList } from '@yandex-int/tap-components/CategoryList';

const App: React.FC = () => {
    const childCategories = [
        { id: 2, name: 'Метки', image: { src: require('./assets/mapiconcolor.png') }},
        { id: 3, name: 'Кошелечки', image: { src: require('./assets/money.png') }},
        { id: 4, name: 'Спиральки', image: { src: require('./assets/eda.png') }},
    ];

    return (
        <CategoryList
            className="my-category-list"
            categories={childCategories}
            parentCategory={{ id: 1, name: 'Фотосток' }}
        />
    );
};
```

## Примеры

### Компонент

{{%story:::tap-components-e-commerce-categorylist--playground%}}

### Скелетон

{{%story:::tap-components-e-commerce-categorylist--skeleton%}}

## Свойства

### Компонент

| Свойство        | Тип                 | Описание                                                  |
| --------------- | ------------------- | --------------------------------------------------------- |
| allItemText?    | `string`            | Текст для ссылки на товары родительской категории         |
| categories      | `Array<Category>`   | Данные подкатегорий                                       |
| className?      | `string`            | Дополнительный класс у корневого DOM-элемента             |
| parentCategory? | `Category`          | Родительская категория                                    |
| title?          | `React.ReactNode`   | Заголовок списка категорий. По умолчанию `category.name`  |
| titleTag?       | `React.ElementType` | Тэг, которым будет отрисован заголовок, по умолчанию `h2` |

```typescript jsx
type ID = string | number;

type Category = {
    id: ID;
    name: string;
    image?: {
        src?: string;
        src2x?: string;
    };
    linkComponent?: React.ComponentType;
};
```

#### Category

| Свойство       | Тип                   | Описание                                      |
| -------------- | --------------------- | --------------------------------------------- |
| id             | `ID`                  | Идентификатор категории                       |
| image?         | `CategoryImage`       | Изображение категории                         |
| linkComponent? | `React.ComponentType` | Компонент для оборачивания категории в ссылку |
| name           | `string`              | Название категории                            |

### Скелетон

| Свойство    | Тип        | Описание                                      |
| ----------- | ---------- | --------------------------------------------- |
| className?  | `string`   | Дополнительный класс у корневого DOM-элемента |
| count?      | `number`   | Количество скелетонов элементов списка        |
| withTitle?  | `boolean`  | Отвечает за отрисовку скелетона заголовка     |

## CSS-переменные

### Компонент

| Переменная                              | Тип     | Описание                              |
| --------------------------------------- | ------- | ------------------------------------- |
| --category-list-all-items-link-bg-color | `color` | Цвет фона логотипа категорий в списке |

### Скелетон

| Переменная                             | Тип      | Описание                            |
| -------------------------------------- | -------- | ----------------------------------- |
| --category-list-skeleton-title-margin  | `margin` | Внешние отступы скелетона заголовка |
