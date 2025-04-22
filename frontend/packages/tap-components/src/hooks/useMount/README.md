# useMount

Позволяет выполнить эффект только при mount и unmount компонента.

## Пример использования

```typescript jsx
import React from 'react';
import { useMount } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    useMount(() => {
        console.log('Mount');

        return () => {
            console.log('Unmount');
        };
    });

    return null;
};
```

## Пример

{{%story:::tap-components-hooks-usemount--playground%}}

## Параметры

```typescript jsx
import { EffectCallback } from 'react';

function useMount(effect: EffectCallback): void;
```

| Свойство | Тип              | Описание                                |
| -------- | ---------------- | --------------------------------------- |
| effect   | `EffectCallback` | Функция, вызываемая на mount компонента |
