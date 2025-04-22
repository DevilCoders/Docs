# useDeferredEffect

Используется для отложенного запуска эффекта:

- Запуск эффекта происходит, когда isEffectLocked выставится в false.
- Не запускает эффект, если его зависимотси не изменились.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { useDeferredEffect } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const [isAuthorized, authorize] = useState(false);
    const [count, setCount] = useState(0);

    useDeferredEffect(!isAuthorized, () => {
        setCount(prevCount => prevCount + 1);
    }, []);

    return (
        <>
            <button onClick={() => { authorize(!isAuthorized) }}>
                {isAuthorized ? 'Выйти' : 'Авторизоваться'}
            </button>
            <div>Количество запусков хука: {count}</div>
        </>
    );
};
```

## Пример

{{%story:::tap-components-hooks-usedeferredeffect--playground%}}

## Параметры

```typescript jsx
import { EffectCallback, DependencyList } from 'react';

function useDeferredEffect(isEffectLocked: boolean, effect: EffectCallback, effectDeps: DependencyList): void;
```

| Свойство       | Тип              | Описание                                                      |
| -------------- | ---------------- | ------------------------------------------------------------- |
| effect         | `EffectCallback` | Эффект. Функция, которая выполняется внутри `React.useEffect` |
| effectDeps     | `DependencyList` | Массив зависимостей эффекта `effect`                          |
| isEffectLocked | `boolean`        | Условие запуска эффекта                                       |
