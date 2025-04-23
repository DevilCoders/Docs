# Label

Компонент-лейбл. Позволяет настроить цвет фона, жирность и цвет текста.

## Пример использования

```typescript jsx
import React from 'react';
import { Label } from '@yandex-int/tap-components/Label';

const App: React.FC = () => {
    return  (
        <Label>Заявка отправлена</Label>
    );
};
```

### Скелетон

```typescript jsx
import React from 'react';
import { LabelSkeleton } from '@yandex-int/tap-components/Label';

const App: React.FC = () => {
    return <LabelSkeleton className="my-label" />;
};
```

## Примеры

### Компонент

{{%story:::tap-components-components-label--playground%}}

### Скелетон

{{%story:::tap-components-components-label--skeleton%}}

## CSS-переменные

| Переменная          | Тип           | Описание               |
| ------------------- | ------------- | ---------------------- |
| --label-color       | `color`       | Цвет текста лейбла     |
| --label-font-weight | `font-weight` | Жирность текста лейбла |
| --label-bg-color    | `color`       | Цвет фона лейбла       |
