# Slider

Компонент-листалка. 

С его помощью можно:

- Пролистывать дочерние элементы свайпом.
- Останавливаться ровно на середине дочернего элемента.
- Отрендериться с изначальным показом заданного элемента (слайда).

## Пример использования

```typescript jsx
import React from 'react';
import { Slider } from '@yandex-int/tap-components/Slider';

const slides = [
    { src: 'image1-1x.png', src2x: 'image1-2x.png' },
    { src: 'image2-1x.png', src2x: 'image2-2x.png' },
    { src: 'image3-1x.png', src2x: 'image3-2x.png' },
];

const App: React.FC = () => {
    return  (
        <Slider className="my-slider" activeIndex={2} >
            {slides.map((slide, index) => (
                <img
                    key={`item-${index}`}
                    src={slide.src}
                    srcSet={`${slide.src2x} 2x`}
                />
            ))}
        </Slider>
    );
};
```

## Пример

{{%story:::tap-components-components-slider--playground%}}

## Свойства

| Свойство             | Тип                         | Описание                                                  |
| -------------------- | --------------------------- | --------------------------------------------------------- |
| activeIndex?         | `number`                    | Номер стартового слайда                                   |
| children             | `Array<React.ReactNode>`    | Элементы слайдов                                          |
| className?           | `string`                    | Дополнительный класс у корневого DOM-элемента             |
| horizontalScrollRef? | `RefObject<HTMLDivElement>` | Ref-ссылка на элемент с горизонтальным скроллом           |
| immediateScroll?     | `boolean`                   | Включает мгновенное прокручивание при смене `activeIndex` |
| onSlideChange?       | `(index: number) => void`   | Обработчик смены активного слайда                         |

## Поддержка

Для работы в старых версиях браузера необходим [полифил](https://github.com/w3c/IntersectionObserver/tree/master/polyfill) для `IntersectionObserver`

Поддержка без полифила:

Safari >= 11 \
Chrome >= 52
