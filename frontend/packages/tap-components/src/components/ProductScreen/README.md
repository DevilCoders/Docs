# ProductScreen

Компонент экрана товара.

В зависимости от переданных свойств компонент экрана товара может быть отрисован со следующими элементами:

- шапка экрана, залипающая сверху и появляющаяся при скролле;
- информация о товаре;
- настройка товара;
- кнопка добавления товара в корзину;
- дополнительная информация о товаре;
- список магазинов, в которых товар в наличии;
- связанные товары;
- список ссылок;
- рекомендованные товары;
- блок, залипающий внизу экрана.

## Пример использования

```typescript jsx
import React from 'react';
import { Link } from 'react-router-dom';
import { compose, composeU } from '@bem-react/core';

import { Button as ButtonBase, withSizeM, withViewAction } from '@yandex-int/tap-components/Buttons';
import { Gallery } from '@yandex-int/tap-components/Gallery';
import { Header } from '@yandex-int/tap-components/Header';
import { HorizontalScroll } from '@yandex-int/tap-components/HorizontalScroll';
import { List, ListItem } from '@yandex-int/tap-components/List';
import { InfiniteScrollGrid } from '@yandex-int/tap-components/InfiniteScrollGrid';
import {
    ProductCard as ProductCardBase,
    ProductCardSkeleton as ProductCardSkeletonBase,
    withSizeS,
    withSizeM,
    withSkeletonSizeM
} from '@yandex-int/tap-components/ProductCard';
import { ProductInfo } from '@yandex-int/tap-components/ProductInfo';
import { ProductMainAction } from '@yandex-int/tap-components/ProductMainAction';
import { ProductScreen } from '@yandex-int/tap-components/ProductScreen';
import { ProductShops } from '@yandex-int/tap-components/ProductShops';
import { ProductsSection } from '@yandex-int/tap-components/ProductsSection';
import { SectionHeader } from '@yandex-int/tap-components/SectionHeader';
import { ShopList, Shop as ShopBase, withShopControlButton } from '@yandex-int/tap-components/ShopList';

const Button = compose(withSizeM, withViewAction)(ButtonBase);
const ProductCard = composeU(withSizeS, withSizeM)(ProductCardBase);
const ProductCardSkeleton = compose(withSkeletonSizeM)(ProductCardSkeletonBase);
const Shop = compose(withShopControlButton)(ShopBase);

function ProductCardSizeM(props: Omit<React.ComponentProps<typeof ProductCard>, 'size'>) {
    return <ProductCard {...props} size="m" />;
}

const MyProductScreen: React.FC = () => {
    const product = {
        name: 'Кроссовки мужские черные',
        description: 'Сделаны из наутральной кожи, непромокаемые',
        gallery: [
            { src: '/images/1/1' },
            { src: '/images/1/2' },
            { src: '/images/1/3' },
            { src: '/images/1/4' }
        ],
        price: {
            current: '1 200 ₽',
            old: '12 000 ₽',
        },
        brand: {
            id: '1',
            name: 'Adidas'
        }
    };
    const shops = [
        {
            id: '1',
            title: 'ТРК Авиапарк',
            address: 'Ленинградское шоссе, 16А, стр. 4'
        },
        {
            id: '2',
            title: 'ТЦ Аврора Плаза',
            address: 'ул. Льва Толстого, 16'
        }
    ];
    const recommendedProducts = {
        items: [
            {
                title: 'Куртка мужская',
                image: { src: '/images/1' }
            },
            {
                title: 'Кроссовки женские',
                image: { src: '/images/2' }
            },
            {
                title: 'Куртка женская',
                image: { src: '/images/3' }
            },
            {
                title: 'Кроссовки мужские',
                image: { src: '/images/4' }
            }
        ],
        isLoading: false,
        paging: {
            pageSize: 10,
            hasMore: true,
            isLoadingMore: false,
            onLoadMore: () => console.log('Loading more!'),
        }
    };
    const relatedProducts = [
        {
            id: '1',
            title: 'Кроссовки мужские белые',
            image: { src: '/images/3' }
        }
    ];
    const city = { name: 'Москва' };

    const onCartButtonClick = (shopId?: string) => () => {
        console.log(shopId ? `Added product in shop with id ${shopId}` : 'Added product');
    };

    return (
        <ProductScreen
            header={<Header title={product.name} backwardButton={<div>←</div>} />}
            info={(
                <ProductInfo
                    name={product.name}
                    description={product.description}
                    gallery={<Gallery items={product.gallery} />}
                    price={product.price}
                    brand={(
                        <Link to={`/brand/${product.brand.id}`}>
                            {product.brand.name}
                        </Link>
                    )}
                />
            )}
            buttons={(
                <Button size="m" view="action" onClick={onCartButtonClick()}>
                    В корзину
                </Button>
            )}
            shops={(
                <ProductShops
                    title="Отложить в магазине"
                    shopList={(
                        <ShopList>
                            {shops.map(shop => (
                                <Shop
                                    control="button"
                                    title={shop.title}
                                    address={shop.address}
                                    buttonText="В корзину"
                                    onControlClick={onCartButtonClick(shop.id)}
                                    key={shop.id}
                                />
                            ))}
                        </ShopList>
                    )}
                    cityName={city.name}
                    citySettingsControl={(
                        <Link to="/personal/city">
                            Изменить
                        </Link>
                    )}
                    allShopsControl={(
                        <Link to={`product/${product.id}/shops`}>
                            Все магазины
                        </Link>
                    )}
                />
            )}
            relatedProducts={(
                <ProductsSection
                    header={<SectionHeader title="Другие цвета этой модели" />}
                    products={(
                        <HorizontalScroll>
                            {relatedProducts.map(relatedProduct => <ProductCard key={relatedProduct.id} size="s" {...relatedProduct} />)}
                        </HorizontalScroll>
                    )}
                />
            )}
            links={(
                <List>
                    <ListItem
                        hasArrow
                        linkComponent={({ children }) => (
                            <Link to="/category/krossovki">{children}</Link>
                        )}
                    >
                        Все кроссовки
                    </ListItem>
                    <ListItem
                        hasArrow
                        linkComponent={({ children }) => (
                            <Link to="/category/obuv">{children}</Link>
                        )}
                    >
                        Вся обувь
                    </ListItem>
                </List>
            )}
            recommendedProducts={(
                <ProductsSection
                    header={<SectionHeader title="Рекомендуем" />}
                    products={(
                        <InfiniteScrollGrid
                            items={recommendedProducts.items}
                            isLoading={recommendedProducts.isLoading}
                            paging={recommendedProducts.paging}
                            component={ProductCardSizeM}
                            skeleton={(
                                <>
                                    {[...Array(6)].map((_, index) => (<ProductCardSkeleton key={index} size="m" />))}
                                </>
                            )}
                        />
                    )}
                />
            )}
            stickyBlock={(
                <ProductMainAction
                    price={product.price}
                    button={(
                        <Button size="m" view="action" onClick={onCartButtonClick}>
                            В корзину
                        </Button>
                    )}
                />
            )}
        />
    );
};
```

## Пример

{{%story:::tap-components-screens-productscreen--playground%}}

## Свойства

| Свойство             | Тип               | Описание                                                                      | Рекомендуемые компоненты |
| -------------------- | ----------------- | ----------------------------------------------------------------------------- | ------------------------ |
| additionalInfo?      | `React.ReactNode` | Блок дополнительной информации о товаре                                       |                          |
| buttons              | `React.ReactNode` | Блок кнопок товара                                                            | `Button`                 |
| className?           | `string`          | Дополнительный класс у корневого DOM-элемента                                 |                          |
| header?              | `React.ReactNode` | Шапка экрана, залипает вверху экрана; появляется, когда экран проскроллен     | `Header`                 |
| info                 | `React.ReactNode` | Блок информации о товаре                                                      | `ProductInfo`            |
| links?               | `React.ReactNode` | Блок ссылок                                                                   | `List`                   |
| settings?            | `React.ReactNode` | Блок настройки свойств товара, например выбора размера или цвета              |                          |
| shops?               | `React.ReactNode` | Блок магазинов, где товар в наличии                                           | `ProductShops`           |
| stickyBlock?         | `React.ReactNode` | Блок, залипающий внизу экрана; появляется после прокрутки блока кнопок товара | `ProductMainAction`      |
| recommendedProducts? | `React.ReactNode` | Блок рекомендованных товаров                                                  | `ProductsSection`        |
| relatedProducts?     | `React.ReactNode` | Блок связанных товаров                                                        | `ProductsSection`        |

## CSS-переменные

| Переменная                           | Тип       | Описание                                 |
| ------------------------------------ | --------- | ---------------------------------------- |
| --product-screen-bg-color            | `color`   | Цвет фона экрана                         |
| --product-screen-top-padding         | `px`      | Отступ от верха экрана                   |
| --product-screen-side-padding        | `px`      | Отступ от края экрана слева и справа     |
| --product-screen-bottom-padding      | `px`      | Отступ от низа экрана                    |
| --product-screen-sticky-block-bottom | `px`      | Отступ залипающего блока от низа экрана  |
| --product-screen-header-z-index      | `z-index` | Слой, на котором располагается заголовок |

## Поддержка

Для работы в старых версиях браузера необходим [полифил](https://github.com/w3c/IntersectionObserver/tree/master/polyfill) для `IntersectionObserver`

Поддержка без полифила:

Safari >= 11 \
Chrome >= 52
