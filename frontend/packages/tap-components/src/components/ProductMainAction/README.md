# ProductMainAction

Компонент основного действия с товаром.

С его помощью можно вывести:

- обычную и специальную цену товара;
- кнопку основного действия с товаром (обычно это «Добавить в корзину»).

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { ProductMainAction } from '@yandex-int/tap-components/ProductMainAction';
import {
    Button as ButtonBase,
    withSizeM,
    withViewAction,
    withWidthAuto,
} from '../Button/Button';

const Button = compose(
    withSizeM,
    withViewAction,
    withWidthAuto,
)(ButtonBase);

const App: React.FC = () => {
    return (
        <ProductMainAction
            price={{
                current: '1 200 ₽',
                old: '12 000 ₽',
            }}
            button={(
                <Button
                  size="m"
                  view="action"
                  width="auto"
                  onClick={() => console.log('Clicked!')}
                >
                    В корзину
                </Button>
            )}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-productmainaction--playground%}}

## Свойства

| Свойство   | Тип               | Описание                                      |
| ---------- | ----------------- | --------------------------------------------- |
| button     | `React.ReactNode` | Кнопка основного действия                     |
| className? | `string`          | Дополнительный класс у корневого DOM-элемента |
| price      | `Price`           | Цена товара                                   |

```typescript
type Price = {
    current: React.ReactNode;
    old?: React.ReactNode;
};
```

## CSS-переменные

Отображение цены можно настроить с помощью CSS-переменных компонента `Price`.
