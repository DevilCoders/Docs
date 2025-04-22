# CheckoutScreen

Компонент страницы оформления заказа.

Позволяет вывести:

- шапку;
- список магазинов c товарами;
- форму для заполнения контактов;
- блок «Итого».

## Пример использования

```typescript jsx
import React, { useCallback, useState } from 'react';
import { useHistory } from 'react-router-dom';
import { useDispatch } from 'react-redux';
import { compose } from '@bem-react/core';

import { Agreements, useAgreements } from '@yandex-int/tap-components/Agreements';
import { Button as ButtonBase, withSizeM, withViewAction } from '@yandex-int/tap-components/Buttons';
import { CartSummary } from '@yandex-int/tap-components/CartSummary';
import { CheckoutScreen } from '@yandex-int/tap-components/CheckoutScreen';
import { CheckoutSuccessModal } from '@yandex-int/tap-components/CheckoutSuccessModal';
import { ContactsForm, Contacts } from '@yandex-int/tap-components/ContactsForm';
import { Header } from '@yandex-int/tap-components/Header';
import { Image } from '@yandex-int/tap-components/Image';
import { ShopSelect } from '@yandex-int/tap-components/ShopSelect';

const Button = compose(withSizeM, withViewAction)(ButtonBase);

const MyCheckoutScreen: React.FC = () => {
    const history = useHistory();
    const dispatch = useDispatch();

    const [isSuccessModalVisible, setIsSuccessModalVisible] = useState<boolean>(false);

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

    const isSubmitDisabled = !selectedShopId || !isRequiredAgreementsChecked;

    const onOrderCreate = () => console.log('Order created!');

    const onSuccessModalClose = useCallback(() => {
        history.push({ pathname: '/' });
    }, [history, dispatch]);

        const shopsWithProducts = [
        {
            shop: {
                id: '1',
                name: 'ТРК Авиапарк',
                address: 'Ленинградское шоссе, 16А, стр. 4'
            },
            products: [
                { image: { src: 'image1-1x.png', src2x: 'image1-2x.png' }, title: 'Кроссовки' },
                { image: { src: 'image2-1x.png', src2x: 'image2-2x.png' }, title: 'Носки' },
                { image: { src: 'image3-1x.png', src2x: 'image3-2x.png' }, title: 'Зонт' },
            ]
        },
        {
            shop: {
                id: '2',
                name: 'ТЦ Аврора Плаза',
                address: 'ул. Льва Толстого, 16'
            },
            products: [
                { image: { src: 'image1-1x.png', src2x: 'image1-2x.png' }, title: 'Кроссовки' },
                { image: { src: 'image2-1x.png', src2x: 'image2-2x.png' }, title: 'Носки' },
            ]
        }
    ];

    const [selectedShopId, setSelectedShopId] = useState<string | number | null>(null);

    const [contacts, setContacts] = useState<Contacts>({
        name: '',
        phone: '',
        email: ''
    });

    const onContactsChange = (changes: Contacts) => {
        setContacts({ ...contacts, ...changes });
    };

    return (
        <>
            <CheckoutScreen
                header={<Header title="Оформление" backwardLink="/cart" />}
                shopSelect={(
                  <ShopSelect
                      shopsWithProducts={shopsWithProducts}
                      selectedShopId={selectedShopId}
                      totalItemsCount={3}
                      onShopSelect={setSelectedShopId}
                  />
               )}
                contacts={(
                    <ContactsForm
                        contacts={contacts}
                        onChange={onContactsChange}
                    />
                )}
                summary={(
                    <CartSummary
                        properties={(
                            <>
                              <Property name="3 товара на сумму" value="6499 ₽" />
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
                        isSubmitDisabled={isSubmitDisabled}
                        onSubmitClick={onOrderCreate}
                    />
                )}
            />
            <CheckoutSuccessModal
                visible={isSuccessModalVisible}
                image={<Image src="/images/checkout-success" />}
                title="Заказ принят"
                text="Когда магазин подтвердит заказ, мы отправим вам SMS и e-mail с деталями заказа."
                controls={<Button size="m" view="action" onClick={onSuccessModalClose}>Продолжить покупки</Button>}
                onClose={onSuccessModalClose}
            />
        </>
    );
};
```

## Пример

{{%story:::tap-components-screens-checkoutscreen--playground%}}

## Свойства

| Свойство    | Тип               | Описание                                      | Рекомендуемые компоненты |
| ----------- | ----------------- | --------------------------------------------- | ------------------------ |
| header?     | `React.ReactNode` | Шапка экрана                                  | `Header`, `Search`       |
| shopSelect? | `React.ReactNode` | Блок для выбора магазина из списка            | `ShopSelect`             |
| contacts?   | `React.ReactNode` | Форма для заполнения контактов                | `Contacts`               |
| summary     | `React.ReactNode` | Блок итоговой информации о корзине            | `CartSummary`            |
| tip?        | `React.ReactNode` | Подсказка по оформлению заказа                | `MessageBox`             |
| className?  | `string`          | Дополнительный класс у корневого DOM-элемента |                          |

## CSS-переменные

| Переменная                       | Тип     | Описание                                                                         |
| -------------------------------- | ------- | -------------------------------------------------------------------------------- |
| --checkout-screen-bg-color       | `color` | Цвет фона страницы                                                               |
| --checkout-screen-block-bg-color | `color` | Цвет фона блоков страницы (`header`, `tip`, `shopSelect`, `contacts`, `summary`) |
| --checkout-screen-padding        | `px`    | Отступ страницы от края экрана слева и справа                                    |
