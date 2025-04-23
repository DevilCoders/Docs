# FiltersPanel

Блок панели сортировки и фильтрации.

## Пример использования

```typescript jsx
import React, { useCallback } from 'react';
import { FiltersPanel } from '@yandex-int/tap-components/FilterCurrentValue';

const App: React.FC = () => {
    const onFilterClick = useCallback(() => {
        window.location.href = '/filters'
    }, []);

    const onSortingClick = useCallback(() => {
        window.location.href = '/sorting'
    }, []);

    return (
        <FiltersPanel
            filters={{
                count: 2,
                onClick: onFilterClick,
            }}
            sorting={{
                label: 'По названию',
                onClick: onSortingClick,
            }}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-filterspanel--playground%}}

## Свойства

| Свойство   | Тип                       | Описание                                      |
| ---------- | ------------------------- | --------------------------------------------- |
| className? | `string`                  | Дополнительный класс у корневого DOM-элемента |
| filters?   | `FiltersPanelFilters`     | Параметры блока фильтров                      |
| sorting?   | `FiltersPanelSorting`     | Параметры блока сортировки                    |

```typescript jsx
type FiltersPanelFilters = {
    count?: number; // количество выбранных фильтров
    onClick?: (event: SyntheticEvent) => void;

    linkComponent?: React.ComponentType;
    //Компонент, оборачивающий панель фильтров в ссылку
};

type FiltersPanelSorting = {
    label: string; // значение текущей сортировки
    onClick?: (event: SyntheticEvent) => void;

    linkComponent?: React.ComponentType;
    //Компонент, оборачивающий панель сортировки в ссылку
};
```

## CSS-переменные

| Переменная                       | Тип      | Описание                                                              |
| -------------------------------- | -------- | --------------------------------------------------------------------- |
| --filters-panel-bg-color         | `color`  | Цвет фона панели                                                      |
| --filters-panel-bg-counter-color | `color`  | Цвет фона счетчика филтьтров                                          |
| --filters-panel-color            | `color`  | Цвет шрифта панели                                                    |
| --filters-panel-counter-color    | `color`  | Цвет счетчика филтьтров                                               |
| --filters-panel-padding          | `px`     | Значение боковых отступов панели                                      |
| --filters-panel-side-indent      | `px`     | Величина, на которую нужно "вытащить" блок из родителя слева и справа |
