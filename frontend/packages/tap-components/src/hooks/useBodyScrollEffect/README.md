# useBodyScrollEffect

Принимает обработчик, который вызывается на события прокрутки экрана и один раз при инициализации.
В обработчик передается текущая позиция скролла.

## Пример использования

```typescript jsx
import React, { useCallback, useState } from 'react';
import { useBodyScrollEffect } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const [isScreenScrolled, setIsScreenScrolled] = useState(false);
    const onBodyScroll = useCallback(({ scrollPosition }) => {
        setIsScreenScrolled(scrollPosition > 0);
    }, [setIsScreenScrolled]);

    useBodyScrollEffect(onBodyScroll);

  return (
        <div>
            {isScreenScrolled && 'Экран прокручен'}
        </div>
    );
};
```

## Параметры

```typescript jsx
function useBodyScrollEffect(handler: Handler): void;

type ScrollState = {
    scrollPosition: number;
};
type Handler = (state: ScrollState) => void
```

| Свойство | Тип                             | Описание                                 |
| -------- | ------------------------------- | ---------------------------------------- |
| handler  | `(state: ScrollState) => void;` | Функция, вызываемая на событие прокрутки |
