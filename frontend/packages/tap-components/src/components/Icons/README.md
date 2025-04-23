# Icons

Компонент для вставки иконки.

## Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import {
  Icons as IconsBase,
  withGlyphTypeArrow,
} from '@yandex-int/tap-components/Icons';

const Icons = compose(withGlyphTypeArrow)(IconsBase);

const App: React.FC = () => {
    return <Icons glyph="type-arrow" />
};
```

## Пример

{{%story:::tap-components-components-icons--playground%}}

## Свойства

| Свойство   | Тип                                                  | По умолчанию | Описание                                                         |
| ---------- | ---------------------------------------------------- | ------------ | ---------------------------------------------------------------- |
| children?  | `ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)>` | — | Контент иконки |
| className? | `string`                                              | —            | Дополнительный класс у корневого DOM-элемента                    |
| direction? | `"left" \| "top" \| "right" \| "bottom"`              | —            | Направление для иконки-стрелки                                   |
| onClick?   | `(event: MouseEventHandler<HTMLSpanElement>) => void` | —            | Обработчик, который вызывается при нажатии на иконку             |
| size?      | `"ns" \| "xs" \| "s" \| "m" \| "n" \| "l" \| "head"`  | —            | Размер иконки                                                    |
| style?     | `CSSProperties`                                       | `{}`         | CSS-стили иконки                                                 |
| title?     | `string`                                              | —            | Всплывающая подсказка                                            |
| url?       | `string`                                              | —            | Ссылка на изображение или содержимое картинки в кодировке base64 |
