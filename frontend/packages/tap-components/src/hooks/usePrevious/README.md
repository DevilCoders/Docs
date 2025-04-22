# usePrevious

Возвращает предыдущее значение. При первом рендере возвращает `undefined`.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { usePrevious } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const [value, setValue] = useState(0);
    const previousValue = usePrevious(value);

    return null;
};
```

## Пример

{{%story:::tap-components-hooks-useprevious--playground%}}

## Параметры

```typescript jsx
function usePrevious(value: any): any;
```

| Свойство | Тип   | Описание                  |
| -------- | ----- | ------------------------- |
| value    | `any` | Текущее значение в стейте |
