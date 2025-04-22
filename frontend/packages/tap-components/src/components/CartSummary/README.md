# CartSummary

Компонент с итоговой информацией о корзине.

Позволяет вывести:

- строки с итоговой информацией о корзине;
- чекбоксы согласия с правилами и условиями;
- кнопку перехода к оформлению заказа.

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';

import { Agreements, useAgreements } from '@yandex-int/tap-components/Agreements';
import { Button as ButtonBase, withSizeM, withViewAction, withWidthMax } from '@yandex-int/tap-components/Button';
import { CartSummary } from '@yandex-int/tap-components/CartSummary';

const Button = compose(withSizeM, withViewAction, withWidthMax)(ButtonBase);

const App: React.FC = () => {
    const { agreements, isRequiredAgreementsChecked, onAgreementCheck } = useAgreements([
        {
            text: 'Я согласен с правилами бронирования магазина',
            isChecked: false,
            isRequired: true
        },
        {
            text: 'Я согласен на передачу данных в ООО «Магазин»',
            isChecked: false,
            isRequired: true
        },
        {
            text: 'Я хочу получать информацию об акциях магазина (опционально)',
            isChecked: false,
            isRequired: false
        },
    ]);

    return (
        <CartSummary
            properties={(
                <>
                    <Property name="5 товаров на сумму" value="6499 ₽" />
                    <Property name="Услуга самовывоза" value="Бесплатно" />
                    <Property name="Будет начислено бонусов" value="245" />
                    <Property name="Оплата" value="При получении" />
                </>
            )}
            agreements={(
                <Agreements
                    agreements={agreements}
                    onAgreementCheck={onAgreementCheck}
                />
            )}
            submit={(
                <Button
                    size="m"
                    theme="action"
                    width="max"
                    disabled={!isRequiredAgreementsChecked}
                    onClick={() => console.log('Submitted!')}
                >
                    Завершить оформление
                </Button>
            )}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-cartsummary--playground%}}

## Свойства

| Свойство          | Тип               | Описание                                                                      | Рекомендуемые компоненты |
| ----------------- | ----------------- | ----------------------------------------------------------------------------- | ------------------------ |
| properties        | `React.ReactNode` | Блок с итоговой информацией о корзине                                         | Список `Property`        |
| agreements?       | `React.ReactNode` | Блок с чекбоксами согласия с правилами и условиями                            | `Agreements`             |
| className?        | `string`          | Дополнительный класс у корневого DOM-элемента                                 |                          |
| submit?           | `() => void`      | Обработчик нажатия кнопки подтверждения                                       |                          |

## CSS-переменные

| Переменная                     | Тип     | Описание               |
| ------------------------------ | ------- | ---------------------- |
| --cart-summary-separator-color | `color` | Цвет линии-разделителя |
