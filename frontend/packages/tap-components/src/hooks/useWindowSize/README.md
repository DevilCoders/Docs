# useWindowSize

Возвращает размеры экрана. Вызывается на любое изменение высоты и/или ширины окна.

## Пример использования

```typescript jsx
import React from 'react';
import { useWindowSize } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const { height, width } = useWindowSize();
    const isLandscape = width > height;

    return (
        <div>
            {isLandscape && 'Сервис не поддерживает альбомную ориентацию'}
        </div>
    );
};
```

## Пример

{{%story:::tap-components-hooks-usewindowsize--playground%}}

## Параметры

```typescript jsx
function useWindowSize(): { height: number, width: number; };
```
