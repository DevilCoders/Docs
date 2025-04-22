# CheckoutSuccessModal

Модальное окно успешного оформления заказа.

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';

import { Button as ButtonBase, withSizeM, withViewAction } from '@yandex-int/tap-components/Button';
import { CheckoutSuccessModal } from '@yandex-int/tap-components/CheckoutSuccessModal';
import { Image } from '@yandex-int/tap-components/Image';

const Button = compose(withSizeM, withViewAction)(ButtonBase);

const App: React.FC = () => {
    return (
        <CheckoutSuccessModal
            visible
            image={<Image src="/images/checkout-success" />}
            title="Заказ принят"
            text="Когда магазин подтвердит заказ, мы отправим вам SMS и e-mail с деталями заказа."
            controls={<Button size="m" view="action">Продолжить покупки</Button>}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-checkoutsuccessmodal--playground%}}

## Свойства

| Свойство       | Тип               | Описание                                          | Рекомендуемые компоненты   |
| -------------- | ----------------- | ------------------------------------------------- | -------------------------- |
| className?     | `string`          | Дополнительный класс у корневого DOM-элемента     |                            |
| controls?      | `React.ReactNode` | Контролы окна                                     | `Button`                   |
| image?         | `React.ReactNode` | Изображение вверху окна                           |                            |
| onClose?       | `() => void`      | Обработчик закрытия модального окна               |                            |
| order?         | `React.ReactNode` | Информация о сделанном заказе                     | `OrderInfo`                |
| promo?         | `React.ReactNode` | Промо-блок. Например, информация о карте магазина | `MessageBox`               |
| text?          | `React.ReactNode` | Текст окна                                        |                            |
| title?         | `string`          | Заголовок окна                                    |                            |
| unorderedCart? | `React.ReactNode` | Блок с частью корзины, которая не вошла в заказ   | `List` с `CartProductItem` |
| visible        | `boolean`         | Видно ли сейчас модальное окно                    |                            |
