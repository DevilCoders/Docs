# Price

Текущая и старая цена товара.

## Пример использования

### Использование с необходимым набором свойств

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { Price as PriceBase, withSizeS } from '@yandex-int/tap-components/Price';

const Price = compose(withSizeS)(PriceBase);

const App: React.FC = () => {
    return (
        <Price size="s" current={10000} />
    );
};
```

### Использование с полным набором свойств

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { Price, Currency, withSizeS } from '@yandex-int/tap-components/Price';

const Price = compose(withSizeS)(PriceBase);

const App: React.FC = () => {
    return (
        <Price
            className="my-price"
            size="s"
            current="10 000 ₽"
            old="20 000 ₽"
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-price--playground%}}

## Свойства

| Свойство   | Тип               | Описание                                      |
| ---------- | ----------------- | --------------------------------------------- |
| className? | `string`          | Дополнительный класс у корневого DOM-элемента |
| current    | `React.ReactNode` | Текущая цена                                  |
| old?       | `React.ReactNode` | Старая цена                                   |
| size?      | `'s' | 'm' | 'l'` | Размер текущей и старой цены                  |

## CSS-переменные

| Переменная                  | Тип     | Описание                                |
| --------------------------- | ------- | --------------------------------------- |
| --price-text-color          | `color` | Цвет текста                             |
| --price-diagonal-line-color | `color` | Цвет линии, перечеркивающей старую цену |
