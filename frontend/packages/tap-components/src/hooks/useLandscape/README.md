# useLandscape

Возвращает `true`, если устройство находится в ландшафтной ориентации, иначе `false`.

## Пример использования

```typescript jsx
import React from 'react';
import { useLandscape } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const isLandscape = useLandscape();

    return (
            <div>
                {isLandscape && 'Сервис не поддерживает альбомную ориентацию'}
            </div>
        );
}
```

## Пример

{{%story:::tap-components-hooks-uselandscape--playground%}}

## Параметры

```typescript jsx
function useLandscape(): boolean;
```
