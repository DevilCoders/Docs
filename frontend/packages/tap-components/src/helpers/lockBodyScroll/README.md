# lockBodyScroll

Замораживает скролл на `body`.

## Пример использования

```typescript jsx
import { useEffect } from 'react';
import { useSelector } from 'react-redux';
import { lockBodyScroll, getLockBodyScrollState } from '@yandex-int/tap-components/helpers';

import { isMenuVisibleSelector } from './redux/slices/menu';

// Замораживаем скролл на странице, если открыто меню
// Аналогично размораживаем его, если меню скрыто
export function useBodyScrollLock() {
    const isMenuVisible = useSelector(isMenuVisibleSelector);

    useEffect(() => {
        lockBodyScroll(isMenuVisible);
    }, [isMenuVisible]);
}
```

## Параметры

```typescript jsx
function lockBodyScroll(lock: boolean): void;
```

| Свойство | Тип       | Описание                                          |
| -------- | --------- | ------------------------------------------------- |
| lock     | `boolean` | Опция для активации/деактивации заморозки скролла |

```typescript jsx
function getLockBodyScrollState(): { isLocked: boolean, scrollPosition: number };
```

| Свойство       | Тип       | Описание                                 |
| -------------- | --------- | ---------------------------------------- |
| isLocked       | `boolean` | Состояние скролла (заморожен/разморожен) |
| scrollPosition | `number`  | Позиция скролла на момент заморозки      |

