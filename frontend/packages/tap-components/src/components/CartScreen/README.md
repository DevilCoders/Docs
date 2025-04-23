# CartScreen

Компонент экрана корзины товаров.

Позволяет вывести:

- список товаров в корзине;
- блок с итоговой информацией о корзине;
- произвольный блок в конце экрана.

## Пример использования

```typescript jsx
import React, { useCallback, useState } from 'react';
import { compose } from '@bem-react/core';

import { Button as ButtonBase, withSizeM, withViewAction } from '@yandex-int/tap-components/Buttons';
import { CartProductItem } from '@yandex-int/tap-components/CartProductItem';
import { CartScreen } from '@yandex-int/tap-components/CartScreen';
import { CartSummary } from '@yandex-int/tap-components/CartSummary';
import { ContextMenuModal } from '@yandex-int/tap-components/ContextMenuModal';
import { CountSelect } from '@yandex-int/tap-components/CountSelect';
import { CountSelectModal } from '@yandex-int/tap-components/CountSelectModal';
import { Header } from '@yandex-int/tap-components/Header';
import { HorizontalScroll } from '@yandex-int/tap-components/HorizontalScroll';
import { List, ListItem } from '@yandex-int/tap-components/List';
import { Notification } from '@yandex-int/tap-components/Notification';
import { ProductCard as ProductCardBase, withSizeS } from '@yandex-int/tap-components/ProductCard';
import { ProductsSection } from '@yandex-int/tap-components/ProductsSection';
import { Property } from '@yandex-int/tap-components/Property';
import { SectionHeader } from '@yandex-int/tap-components/SectionHeader';

const Button = compose(withSizeM, withViewAction)(ButtonBase);
const ProductCard = compose(withSizeS)(ProductCardBase);

const MAX_CART_COUNT = 10;

const MyCartScreen: React.FC = () => {
    const [notification, setNotification] = useState<string | null>(null);
    const onNotificationClose = useCallback(() => setNotification(null), []);

    const onRemoveAll = () => console.log('Remove all clicked!');

    const [contextModalItemIndex, setContextModalItemIndex] = useState<number | null>(null);

    const onContextMenuClose = () => setContextModalItemIndex(null);

    const [isCountSelectModalVisible, setIsCountSelectModalVisible] = useState(false);
    const [countSelectCount, setCountSelectCount] = useState(0);

    const cartItems = [
        {
            product: {
                image: { src: '/images/1' },
                title: 'Кроссовки мужские',
                price: {
                    current: '3 200 ₽',
                },
            },
            onContextMenuClick: () => setContextModalItemIndex(0)
        },
        {
            product: {
                image: { src: '/images/2' },
                title: 'Кроссовки женские',
                price: {
                    current: '2 800 ₽',
                },
            },
            onContextMenuClick: () => setContextModalItemIndex(1)
        },
    ];
    const [counts, setCounts] = useState<Array<number>>([1, 1]);

    const recommendedProducts = [
        {
            id: '1',
            title: 'Туфли мужские',
            image: { src: '/images/3' }
        },
        {
            id: '2',
            title: 'Туфли женские',
            image: { src: '/images/4' }
        },
    ];

    const onChangeCountClick = () => {
        setIsCountSelectModalVisible(true);
        setCountSelectCount(counts[contextModalItemIndex]);
    };

    const onCountSelect = (count: number) => {
        const newCounts = counts.slice();

        newCounts[contextModalItemIndex] = count;

        setCounts(newCounts);
        setContextModalItemIndex(null);
        setIsCountSelectModalVisible(false);
    };

    const onRemoveClick = () => onCountSelect(0);

    const cartCount = counts.reduce((sum, count) => sum + count, 0);

    const onCheckoutClick = () => {
        if (cartCount > MAX_CART_COUNT) {
            setNotification('Слишком много вещей, удалите часть из них');

            return;
        }
    };

    return (
        <>
            <CartScreen
                header={<Header
                    title="Корзина"
                    end={<div onClick={onRemoveAll}>🗑️</div>}
                />}
                cart={(
                    <List>
                        {cartItems.map((item, index) => (
                            <ListItem key={index}>
                                <CartProductItem {...item}>
                            </ListItem>
                        ))}
                    </List>
                )}
                summary={<CartSummary
                    properties={(
                        <>
                            <Property name={`${cartCount} товаров на сумму`} value={`${cartCount * 3000} ₽`} />
                            <Property name="Услуга самовывоза" value="Бесплатно" />
                            <Property name="Будет начислено бонусов" value="245" />
                            <Property name="Оплата" value="При получении" />
                        </>
                      )}
                    submit={<Button size="m" view="action" onClick={onCheckoutClick}>Перейти к оформлению</Button>}
                />}
                addonAfter={<ProductsSection
                    header={<SectionHeader title="Рекомендуем" />}
                    products={(
                        <HorizontalScroll>
                            {recommendedProducts.map(product => <ProductCard key={product.id} size="s" {...product} />)}
                        </HorizontalScroll>
                    )}
                />}
            />
            <ContextMenuModal
                visible={contextModalItemIndex !== null}
                onClose={onContextMenuClose}
            >
                <ListItem onClick={onChangeCountClick}>
                    Изменить количество
                </ListItem>
                <ListItem onClick={onRemoveClick}>
                    Удалить из корзины
                </ListItem>
            </ContextMenuModal>
            <CountSelectModal
                visible={isCountSelectModalVisible}
                title="Количество"
                countSelect={<CountSelect count={countSelectCount} onChange={setCountSelectCount} />}
                controls={<Button size="m" view="action" onClick={onCountSelect}>Выбрать</Button>}
                onClose={onContextMenuClose}
            />
            {notification && (
                <Notification timeout={3000} onClose={onNotificationClose}>
                    {notification}
                </Notification>
            )}
        </>
    );
};
```

## Пример

{{%story:::tap-components-screens-cartscreen--playground%}}

## Свойства

| Свойство    | Тип               | Описание                                      | Рекомендуемые компоненты   |
| ----------- | ----------------- | --------------------------------------------- | -------------------------- |
| cart        | `React.ReactNode` | Блок товаров в корзине                        | `List` с `CartProductItem` |
| summary     | `React.ReactNode` | Блок итоговой информации о корзине            | `CartSummary`              |
| addonAfter? | `React.ReactNode` | Блок в конце экрана                           | `ProductsSection`          |
| className?  | `string`          | Дополнительный класс у корневого DOM-элемента |                            |

## CSS-переменные

| Переменная                   | Тип       | Описание                                 |
| ---------------------------- | --------- | ---------------------------------------- |
| --cart-screen-bg-color       | `color`   | Цвет фона страницы                       |
| --cart-screen-top-padding    | `px`      | Отступ от края экрана сверху             |
| --cart-screen-side-padding   | `px`      | Отступ от края экрана слева и справа     |
| --cart-screen-bottom-padding | `px`      | Отступ от края экрана снизу              |
| --cart-screen-header-z-index | `z-index` | Слой, на котором располагается заголовок |

## Поддержка

Chrome >= 56
