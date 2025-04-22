# ErrorScreen

Экран заглушки при фатальной ошибке в приложении.

## Пример использования

### Использование с необходимым набором свойств

```typescript jsx
import React from 'react';
import { ErrorScreen } from '@yandex-int/tap-components/ErrorScreen';

const App: React.FC = () => {
    return <ErrorScreen />;
};
```

### Использование с полным набором свойств

```typescript jsx
import React from 'react';
import { ErrorScreen } from '@yandex-int/tap-components/ErrorScreen';

const App: React.FC = () => {
    const error = new Error('Test');
    const errorInfo: React.ErrorInfo = {
        componentStack: '...'
    };

    return <ErrorScreen error={error} errorInfo={errorInfo} />;
};
```

## Пример

{{%story:::tap-components-screens-errorscreen--playground%}}

## Свойства

| Свойство   | Тип               | Описание                                 |
| ---------- | ----------------- | ---------------------------------------- |
| error?     | `Error`           | Ошибка, стектрейс которой нужно показать |
| errorInfo? | `React.ErrorInfo` | Информация об ошибке из ErrorBoundary    |

## CSS-переменные

| Переменная          | Тип     | Описание  |
| ------------------- | ------- | --------- |
| --discount-bg-color | `color` | Цвет фона |
