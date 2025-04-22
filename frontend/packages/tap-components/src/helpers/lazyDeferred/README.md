# lazyDeferred

Аналог `React.lazy` с фиксом нескольких проблем:
- Начинает импортировать код спустя некоторое время, чтобы iOS Safari успел отрисовать скелетон. Иначе мобильный Safari рисует белый экран на время загрузки кода.
- Имеет минимальное время загрузки кода, чтобы состояние загрузки не менялось слишком быстро для пользователя.

## Пример использования

```typescript jsx
import React, { Suspense } from 'react';
import { lazyDeferred } from '@yandex-int/tap-components/helpers';

const LazyComponent = lazyDeferred(() => import('./Component'));

const Component: React.FC = () => {
    return (
        <Suspense fallback={skeleton}>
            <LazyComponent />
        </Suspense>
    );
};
```

## Параметры

```typescript jsx
import { lazyDeferred } from '@yandex-int/tap-components/helpers';

lazyDeferred(factory);
```

| Свойство | Тип                                                      | Описание                      |
| -------- | -------------------------------------------------------- | ----------------------------- |
| factory  | `<T extends ComponentType>() => Promise<{ default: T }>` | Метод для загрузки компонента |
