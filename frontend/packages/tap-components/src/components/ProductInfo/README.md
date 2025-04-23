# ProductInfo

Компонент информации о товаре. 

С его помощью можно вывести:

- галерею изображений товара;
- название и описание товара, название бренда товара;
- обычную и специальную цену товара, размер скидки.

## Пример использования

```typescript jsx
import React from 'react';
import { Link } from 'react-router-dom';

import { Gallery } from '@yandex-int/tap-components/Gallery';
import { ProductInfo } from '@yandex-int/tap-components/ProductInfo';

const App: React.FC = () => {
    return (
        <ProductInfo
            name="Туфли мужские T.TACCARDI"
            description="Туфли-лоферы для мужчин из линейки T.TACCARDI. Элегантная модель выполнена из матовой искусственной кожи и украшена перфорированным узором и декоративными ремешками. Такая пара будет выигрышно смотреться в сочетании со строгими брюками или классическим пальто."
            backwardButton={<div>←</div>}
            gallery={<Gallery
                items={[
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/2763477/1650e012666c37357faa6cec9fedab53/orig'
                    },
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/1395928/faa4dba20aab21e8ecdea5c0cbe97e93/orig'
                    },
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/1371687/649a04ab7b8ce8f049933c4fc8cde3a2/orig'
                    },
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/1395928/35648abc6cfd66817f58449dbb060cda/orig'
                    },
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/1674596/20a44279d4f3ce2933d8b31b2c35abb0/orig'
                    },
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/1371687/6319cf1eef7c87330343e471800c4998/orig'
                    },
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/475184/49ee9c2fef31918203ed09d0b4f83830/orig'
                    },
                    {
                        src: 'https://avatars.mds.yandex.net/get-bklk/2763477/f91cf43a604fcbf5bdaebe4f9442f417/orig'
                    }
                ]}
            />}
            discount="-90%"
            price={{
                current: '1 200 ₽',
                old: '12 000 ₽',
            }}
            brand={(
                <Link to="/brand/t-taccardi">
                    T.taccardi
                </Link>
            )}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-productinfo--playground%}}

## Свойства

| Свойство        | Тип               | Описание                                      | Рекомендуемые компоненты |
| --------------- | ----------------- | --------------------------------------------- | ------------------------ |
| backwardButton? | `React.ReactNode` | Блок кнопки «Назад»                           |                          |
| brand?          | `React.ReactNode` | Название бренда товара                        |                          |
| className?      | `string`          | Дополнительный класс у корневого DOM-элемента |                          |
| description?    | `React.ReactNode` | Описание товара                               |                          |
| discount?       | `string`          | Текст со скидкой                              |                          |
| gallery?        | `React.ReactNode` | Галерея медиаданных товара                    | `Gallery`                |
| name            | `React.ReactNode` | Название товара                               |                          |
| price?          | `Price`           | Цена товара                                   |                          |

```typescript jsx
type Price = {
    current: React.ReactNode;
    old?: React.ReactNode;
};
```

## CSS-переменные

| Переменная                          | Тип     | Описание                   |
| ----------------------------------- | ------- | -------------------------- |
| --product-info-text-secondary-color | `color` | Дополнительный цвет текста |
