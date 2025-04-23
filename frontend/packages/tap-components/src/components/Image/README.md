# Image

Компонент для анимированной загрузки картинок.

Процесс загрузки картинки:

1. Картинка загружается, пользователь видит `<stub/>`.
1. Картинка загрузилась и плавно отображается поверх `<stub/>`.
1. Картинка отобразилась, `<stub/>` удаляется из DOM.

> **Примечание:**
>
> - Если картинка загружается из кэша, то пользователь увидит сразу картинку без показа `<stub/>`.
> - Если картинку не удалось загрузить, то покажется картинка по умолчанию из свойства `fallbackSrc`.

## Пример использования

```typescript jsx
import React from 'react'
import { Image } from '@yandex-int/tap-components/Image';

// Использование компонента в вашем приложении
const App: React.FC = () => (
  <Image
    src="https://yastatic.net/lego/_/Kx6F6RQnQFitm0qRxX7vpvfP0K0.png"
    src2x="https://yastatic.net/lego/_/Kx6F6RQnQFitm0qRxX7vpvfP0K0.png"
    alt="Alternative text"
  />
)
```

### Ширина, высота и скругления изображения

Чтобы задать ширину, высоту и скругления изображения, используйте свойства `width`, `height` и `borderRadius`.

### Адаптивное изображение

Чтобы задать изображение для ретины `src2x`, или более гибкие свойства для адаптивных изображений, используйте свойства `sizes` и `srcSet`.

### Заглушки для изображений

Компонент состоит из трех частей:

```html
<container>
    <img/>
    <stub/>
</container>
```

```typescript jsx
import React from 'react';
import { Image } from '@yandex-int/tap-components/Image';

const App: React.FC = () => {
    return (
        <Image className="my-image" stub={<MyImageStub/>} />
    );
};
```

### Использование с полным набором свойств

```typescript jsx
import React from 'react';
import { Image } from '@yandex-int/tap-components/Image';

const App: React.FC = () => {
    return (
        <Image
            src="https://example.com/image-1x.png"
            src2x="https://example.com/image-2x.png"
            fallbackSrc="https://example.com/image-fallback.png"
            alt="Image description"
            ariaLabel="Image description"
            className="mix-root-element (container if use 'stub' or image)"
            imageClassName="mix-for-img-tag-only"
            onClick={() => console.log(`I'm picture!`)}
            stub={<MyImageStub />}
        />
    );
};
```

## Пример

{{%story:::tap-components-components-image--playground%}}

## Свойства

| Свойство        | Тип                                               | Описание                                  |
| ----------------| ------------------------------------------------- | ----------------------------------------- |
| alt?            | `string`                                          | Альтернативный текст |
| ariaLabel?      | `string`                                          | Атрибут aria-label |
| borderRadius?   | `string \| number`                                | Скругления изображения |
| className?      | `string`                                          | Дополнительный класс у корневого DOM-элемента |
| fallback?       | `string`                                          | Ссылка на изображение при неудачной загрузке (legacy-свойство) |
| fallbackSrc?    | `string`                                          | Ссылка на изображение при неудачной загрузке |
| height?         | `string \| number`                                | Высота изображения |
| imageClassName? | `string`                                          | Дополнительный класс у изображения |
| innerRef?       | `RefObject<HTMLImageElement>`                     | Ссылка на корневой DOM-элемент компонента |
| loading?        | `"lazy" \| "eager" \| "auto"`                     | Атрибут [loading у изображения](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-loading), по умолчанию `lazy` |
| onClick?        | `(event: MouseEventHandler<HTMLElement>) => void` | Обработчик нажатия на картинку |
| sizes?          | `string`                                          | Набор размеров для создания [адаптивных изображений](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images). Подробнее об атрибуте `sizes` в документации [MDN web docs](https://developer.mozilla.org/ru/docs/Web/HTML/Element/img#attr-sizes). |
| src?            | `string`                                          | Ссылка на изображение |
| src2x?          | `string`                                          | URL картинки для экранов с высокой плотностью пикселей = srcSet: "url 2x". srcSet имеет приоритет. |
| srcSet?         | `string`                                          | Набор источников для создания [адаптивных изображений](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images). Подробнее об атрибуте `srcSet` в документации [MDN web docs](https://developer.mozilla.org/ru/docs/Web/HTML/Element/img#attr-srcset). |
| stub?           | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Компонент для отображения во время загрузки картинки |
| width?          | `string \| number`                                | Ширина изображения |
