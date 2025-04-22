# Agreements

Компонент с чекбоксами согласия с правилами и/или условиями соглашения.

Также содержит хук с логикой отслеживания состояния чекбоксов и определения, все ли обязательные из них выбраны.

## Пример использования

```typescript jsx
import React from 'react';
import { Agreements, useAgreements } from '@yandex-int/tap-components/Agreements';

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
        <>
            <Agreements
                agreements={agreements}
                onAgreementCheck={onAgreementCheck}
            />
            {isRequiredAgreementsChecked ?
                'Можно оформлять заказ' :
                'Нужно согласиться с условиями магазина'
            }
        </>
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-agreements--playground%}}

## Свойства

| Свойство         | Тип                                       | Описание                                                                                                   |
| ---------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| agreements       | `Array<AgreementType>`                    | Описание пунктов-соглашений                                                                                |
| className?       | `string`                                  | Дополнительный класс у корневого DOM-элемента                                                              |
| onAgreementCheck | `(index: number, value: boolean) => void` | Обработчик изменения состояния чекбокса пункта. На вход принимает индекс пункта и устанавливаемое значение |

```typescript jsx
type AgreementType = {
    text: React.ReactNode;
    isChecked: boolean;
    isRequired?: boolean;
};
```

Для получения состояния `agreements` и обработчика `onAgreementCheck` рекомендуется
использовать хук `useAgreements`, передав ему на вход описание и изначальное состояние пунктов.

## CSS-переменные

| Переменная                  | Тип     | Описание                                      |
| --------------------------- | ------- | --------------------------------------------- |
| --agreements-checkbox-color | `color` | Цвет чекбоксов                                |
