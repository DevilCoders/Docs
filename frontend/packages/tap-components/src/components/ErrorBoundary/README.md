# ErrorBoundary

Компонент [предорахнитель](https://ru.reactjs.org/docs/error-boundaries.html) для перехвата ошибок в методе `render`. В случае фатальной ошибки в приложении будет показан экран ошибки с возможностью перезагрузить страницу.

Можно передать свою функцию для логирования ошибок и включить режим `debug`, чтобы на экране отображалась информация об ошибке и стектрейс.

## Пример использования

```typescript jsx
import React from 'react';
import { ErrorBoundary } from '@yandex-int/tap-components/Label';

const App: React.FC = () => {
    return  (
        <ErrorBoundary>
            Экран приложения
        </ErrorBoundary>
    );
};
```

## Пример

{{%story:::tap-components-components-errorboundary--playground%}}

## Свойства

| Свойство | Тип               | По-умолчанию | Описание                             |
| -------- | ------------------|------------- | -------------------------------------|
| children | `React.ReactNode` |              | Компонент, обёрнутый предохранителем |
| debug?   | `boolean`         | `false`      | Расширенный режим для отладки        |
| logError | `logError`        |              | Функция для логирования ошибки       |

```typescript jsx
type ErrorInfo = {
    message: string;
    type: 'render';
    additional: React.ErrorInfo;
};

type logError = (errorInfo: ErrorInfo, error: Error) => void;
```
