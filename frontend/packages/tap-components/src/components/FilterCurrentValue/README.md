# FilterCurrentValue

Блок отображения текущей фильтрации по определенному свойству.

## Пример использования

```typescript jsx
import React, { useMemo } from 'react';
import { FilterCurrentValue } from '@yandex-int/tap-components/FilterCurrentValue';

const App: React.FC = () => {
    const filterCurrentValueProps = useMemo(() => {
        const linkComponent: React.FC = ({ children }) => {
            return <Link to={'/shop-change'}>{children}</Link>;
        };

        return { linkComponent, label: 'Наличие' };
    }, []);

    return (
        <FilterCurrentValue
            className="my-shop-changer"
            {...filterCurrentValueProps}
        >
            2 из 10
        </FilterCurrentValue>
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-filtercurrentvalue--playground%}}

## Свойства

| Свойство       | Тип                               | Описание                                                             |
| -------------- | --------------------------------- | -------------------------------------------------------------------- |
| className?     | `string`                          | Дополнительный класс у корневого DOM-элемента                        |
| children?      | `React.ReactNode`                 | Значение свойства                                                    |
| icon?          | `React.ReactNode`                 | Иконка-контрол                                                       |
| label?         | `string`                          | Лейбл названия свойства                                              |
| linkComponent? | `React.ComponentType`             | Компонент, оборачивающий `children` в ссылку. Делает элемент ссылкой |
| onClick?       | `(event: SyntheticEvent) => void` | Обработчик клика по значению фильтра                                 |

## CSS-переменные

| Переменная                   | Тип      | Описание              |
| ---------------------------- | -------- | --------------------- |
| --filter-current-value-color | `color`  | Цвет значения фильтра |
