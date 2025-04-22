# useDelayedVisible

Используется для отложенного показа и скрытия элемента:

- Показывает элемент спустя `showDelay` мс
- Скрывает элемент только после того, как он был показан в течение `minimalShowTime` мс

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { useDelayedVisible } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const [isVisible, show, hide] = useDelayedVisible({
        showDelay: 250,
        minimalShowTime: 750,
    });

    return (
        <>
            <button onClick={show}>
                Показать
            </button>
            <button onClick={hide}>
                Скрыть
            </button>
            {isVisible && <div>Элемент</div>}
        </>
    );
};
```

## Пример

{{%story:::tap-components-hooks-usedelayedvisible--playground%}}

## Параметры

```typescript jsx
type UseDelayedVisibleOptions = {
    showDelay: number; // задержка перед появлением
    minimalShowTime: number; // минимальное время видимости
    deafultValue?: boolean; // виден ли элемент изначально
};

function useDelayedVisible(options: UseDelayedVisibleOptions): boolean;
```

| Свойство | Тип                        | Описание                               |
| -------- | -------------------------- | -------------------------------------- |
| options  | `UseDelayedVisibleOptions` | Настройка задержек появления и скрытия |

## Возвращаемые значения

Массив вида `[isVisible, show, hide]`

| Значение  | Тип          | Описание                               |
| --------- | ------------ | -------------------------------------- |
| isVisible | `boolean`    | Текущее состояние видимости            |
| show      | `() => void` | Метод для показа элемента с задержкой  |
| hide      | `() => void` | Метод для скрытия элемента с задержкой |
