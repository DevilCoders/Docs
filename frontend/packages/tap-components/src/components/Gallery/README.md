# Gallery

Компонент галерея изображений. Позволяет:

- Пролистывать изображения свайпом.
- Останавливаться при пролистывании ровно на середине изображения.
- Отрендериться с изначальным показом заданного изображения.
- Вывести пагинацию в виде точек под текущим изображением.

## Пример использования

### Компонент

```typescript jsx
import React from 'react';
import { Gallery } from '@yandex-int/tap-components/Gallery';

const items = [
    { src: 'image1-1x.png', src2x: 'image1-2x.png' },
    { src: 'image2-1x.png', src2x: 'image2-2x.png' },
    { src: 'image3-1x.png', src2x: 'image3-2x.png' },
];

const App: React.FC = () => {
    return  (
        <Gallery className="my-gallery" items={items} activeIndex={2} />
    );
};
```

### Скелетон

```typescript jsx
import React from 'react';
import { GallerySkeleton } from '@yandex-int/tap-components/Gallery';

const App: React.FC = () => {
    return <GallerySkeleton className="my-gallery" />;
};
```

## Примеры

### Компонент

{{%story:::tap-components-components-gallery--playground%}}

### Скелетон

{{%story:::tap-components-components-gallery--skeleton%}}

## Свойства

| Свойство             | Тип                                                       | Описание                                                  |
| -------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| activeIndex?         | `number`                                                  | Номер стартового элемента                                 |
| className?           | `string`                                                  | Дополнительный класс у корневого DOM-элемента             |
| horizontalScrollRef? | `RefObject<HTMLDivElement>`                               | Ref-ссылка на элемент с горизонтальным скроллом           |
| immediateScroll?     | `boolean`                                                 | Включает мгновенное прокручивание при смене `activeIndex` |
| items                | `Array<GalleryItem>`                                      | Информация об изображениях, в двух размерах               |
| onItemClick?         | `(event: MouseEvent<HTMLElement>, index: number) => void` | Обработчик нажатия на элемент                             |
| onItemChange?        | `(index: number) => void`                                 | Обработчик смены активного элемента                       |

```typescript jsx
type GalleryItem = {
    src: string;
    src2x?: string;
    alt?: string;
};
```

## CSS-переменные

| Переменная                      | Тип     | Описание                      |
| ------------------------------- | ------- | ----------------------------- |
| --gallery-item-height           | `px`    | Высота контейнера изображений |
| --gallery-item-image-bg-color   | `color` | Цвет контейнера изображений   |
| --gallery-item-width            | `px`    | Ширина контейнера изображений |
| --gallery-point-active-bg-color | `color` | Цвет активной точки пагинации |
| --gallery-point-bg-color        | `color` | Цвет точек пагинации          |
| --gallery-point-radius          | `px`    | Радиус точки пагинации        |

## Поддержка

Для работы в старых версиях браузера необходим [полифил](https://github.com/w3c/IntersectionObserver/tree/master/polyfill) для `IntersectionObserver`

Поддержка без полифила:

Safari >= 11 \
Chrome >= 52
