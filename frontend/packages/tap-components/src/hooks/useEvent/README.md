# useEvent

Hook для удобной работы с событиями на DOM-элементе.

## Пример использования

```typescript jsx
import React, { useRef, useCallback } from 'react';
import { useEvent } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const ref = useRef();
    const onScroll = useCallback(() => {
        console.log('scroll');
    }, []);

    useEvent('scroll', onScroll, ref.current);

    return <div ref={ref} />;
};
```

## Параметры

```typescript jsx
function useEvent(
    name: string,
    handler: <T extends Event>(event: T) => void,
    target: EventTarget | null,
    options: AddEventListenerOptions
): void;
```

| Свойство | Тип                                   | Описание                                                 |
| -------- | ------------------------------------- | ---------------------------------------------------------|
| handler  | `<T extends Event>(event: T) => void` | Обработчик события                                       |
| name     | `string`                              | Название события                                         |
| options? | `AddEventListenerOptions`             | Дополнительные опции обработчика событий                 |
| target?  | `EventTarget | null`                  | Элемент для прослушивания события, по умолчанию `window` |
