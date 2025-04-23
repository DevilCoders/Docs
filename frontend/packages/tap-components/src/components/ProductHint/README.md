# ProductHint

Всплывающая подсказка, которая информирует пользователя о том, что товар добавлен в корзину.

## Пример использования

```typescript jsx
import React, { useCallback } from 'react';

import { ProductHint } from '@yandex-int/tap-components/ProductHint';

const Component: React.FC = () => {
    const image = {
        alt: 'image',
        src: 'https://example.com/image@1x.png',
        src2x: 'https://example.com/image@2x.png',
    };

    const onClick = useCallback(() => {
        console.info('Клик по кнопке!');
    }, []);

    return (
        <ProductHint
            className="my-product-hint"
            image={image}
            text="Товар добавлен в корзину"
            handlerText="Оформить"
            onClick={onClick}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-producthint--playground%}}

## Свойства

| Свойство       | Тип                   | Описание                                                                 |
| -------------- | --------------------- | ------------------------------------------------------------------------ |
| buttonText     | `string`              | Текст в кнопке                                                           |
| className?     | `string`              | Дополнительный класс у корневого DOM-элемента                            |
| image          | `ProductHintImage`    | Изображение товара                                                       |
| linkComponent? | `React.ComponentType` | Компонент, оборачивающий кнопку в ссылку; делает элемент целиком ссылкой |
| onClick?       | `() => void`          | Обработчик, который будет вызыван при клике на кнопку                    |
| text           | `string`              | Текст рядом с изображением                                               |

```typescript jsx
type ProductHintImage = {
    src: string;
    src2x?: string;
    alt?: string;
};
```

## CSS-переменные

| Переменная                        | Тип     | Описание                       |
| --------------------------------- | ------- | ------------------------------ |
| --product-hint-bg-color           | `color` | Цвет фона всплывающего окна    |
| --product-hint-text-color         | `color` | Цвет текста во всплывающем окне|
| --product-hint-image-bg-color     | `color` | Цвет заглушки картинки         |
| --product-hint-handler-bg-color   | `color` | Цвет фона кнопки               |
| --product-hint-handler-text-color | `color` | Цвет текста в кнопке           |
