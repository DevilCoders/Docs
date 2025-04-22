# ShopList

Компонент списка магазинов. Может быть отрисован c:

- кнопкой напротив магазина;
- чекбоксами для множественного выбора;
- радиокнопками для единственного выбора.

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';

import { ShopList, Shop as ShopBase, withControlCheckbox } from '@yandex-int/tap-components/ShopList';

const Shop = compose(withControlCheckbox)(ShopBase);

const shops = [
    {
        title: 'Shop 1',
        address: 'Address 1',
    },
    {
        title: 'Shop 2',
        address: 'Address 2',
    },
    {
        title: 'Shop 3',
        address: 'Address 3',
    },
];

const App: React.FC = () => {
    return  (
        <ShopList className="my-shop-list">
            {shops.map((shop, index) => (
                <Shop
                    key={index}
                    title={shop.title}
                    address={shop.address}
                    control="checkbox"
                    onControlClick={() => alert(`Clicked on ${shop.title}!`)}
                    className="my-shop"
                />
            ))}
        </ShopList>
    );
};
```

## Примеры

### Компонент

{{%story:::tap-components-e-commerce-shoplist--playground%}}

### Компонент с разными типами контролов

{{%story:::tap-components-e-commerce-shoplist--controls%}}

## Свойства

| Свойство   | Тип         | Описание                                      |
| ---------- | ----------- | --------------------------------------------- |
| children   | `ReactNode` | Элементы магазинов                            |
| className? | `string`    | Дополнительный класс у корневого DOM-элемента |

## Shop

Вспомогательный компонент для отображения элемента списка магазинов.

### Свойства

| Свойство       | Тип                               | Описание                                                                     |
| -------------- | --------------------------------- | ---------------------------------------------------------------------------- |
| address?       | `string`                          | Адрес магазина                                                               |
| children?      | `ReactNode`                       | Элемент, который будет вставлен в DOM после description                      |
| className?     | `string`                          | Дополнительный класс у корневого DOM-элемента                                |
| control?       | `ControlType`                     | Тип контрола для выбора магазина                                             |
| description?   | `ReactNode`                       | Дополнительные сведения о магазине или товаре                                |
| linkComponent? | `React.ComponentType`             | Компонент, оборачивающий `children` в ссылку. Делает элемент целиком ссылкой |
| onClick?       | `(event: SyntheticEvent) => void` | Обработчик клика на элемент                                                  |
| title          | `string`                          | Название магазина                                                            |

```typescript jsx
type ControlType = 'checkbox' | 'radio' | 'button';
```

### CSS-переменные

| Переменная           | Тип     | Описание               |
| -------------------- | --------| -----------------------|
| --shop-title-color   | `color` | Цвет названия магазина |
| --shop-address-color | `color` | Цвет адреса магазина   |

#### Тип контрола для выбора магазина

Чтобы:

- Изменить элемент для выбора магазина, установите свойство `control` в одно из следующих значений:
`checkbox`, `radio`, `button`.
- Установить значение элемента для выбора магазина, воспользуйтесь свойством `checked` (для `checkbox` и `radio`).
- Установить обработчик на клик по элементу для выбора магазина, воспользуйтесь свойством `onControlClick`.

При использовании `control="button"`, текст кнопки можно задать с помощью свойства `buttonText`.

#### Свойства модификатора

| Свойство        | Тип                                        | Описание                                              |
| --------------- | -------------------------------------------| ----------------------------------------------------- |
| buttonText?     | `string`                                   | Текст кнопки                                          |
| checked?        | `boolean`                                  | Выбран ли магазин                                     |
| onControlClick? | `(event: MouseEvent<HTMLElement>) => void` | Обработчик, который вызывается при нажатии на контрол |
