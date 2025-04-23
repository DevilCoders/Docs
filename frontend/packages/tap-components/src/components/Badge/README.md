# Badge

Значок-счетчик в правом верхнем углу своего дочернего элемента.

## Пример использования

```typescript jsx
import React from 'react';
import { Badge } from '@yandex-int/tap-components/Badge';

const App: React.FC = () => {
    const IconTwo = () => (
        <svg fill="var(--color-control-typo-primary)" xmlns="http://www.w3.org/2000/svg" width="20" height="20"><path d="M4.5 18a.5.5 0 1 1 0-1 .5.5 0 0 1 0 1zm0-3a2.5 2.5 0 0 0 0 5 2.5 2.5 0 0 0 0-5zm11 3a.5.5 0 1 1 0-1 .5.5 0 0 1 0 1zm0-3a2.5 2.5 0 0 0 0 5 2.5 2.5 0 0 0 0-5zM19 4H5.78L4.97.758A.998.998 0 0 0 4 0H1a1 1 0 0 0 0 2h2.22l.805 3.222.01.042 1.995 7.98a1 1 0 0 0 1.135.743l11.017-1.837c1.02-.17 1.818-1.11 1.818-2.14V5a1 1 0 0 0-1-1zm-1 6.01c0 .05-.085.157-.146.167L7.746 11.862 6.28 6H18v4.01z" /></svg>
    );

    return (
        <Badge content={10}>
            <IconTwo />
        </Badge>
    );
};
```

## Пример

{{%story:::tap-components-components-badge--playground%}}

## Свойства

| Свойство      | Тип                         | Описание                                      |
| ------------- | --------------------------- | --------------------------------------------- |
| className?    | `string`                    | Дополнительный класс у корневого DOM-элемента |
| color?        | `string`                    | Цвет заливки блока                            |
| content?      | `string \| number`          | Содержимое, отображаемое внутри значка        |
| innerRef?     | `RefObject<HTMLDivElement>` | Ссылка на корневой DOM-элемент компонента     |
| outlineColor? | `string`                    | Цвет обводки блока                            |
| style?        | `CSSProperties`             | Пользовательские стили                        |
| textColor?    | `string`                    | Цвет текста блока                             |
