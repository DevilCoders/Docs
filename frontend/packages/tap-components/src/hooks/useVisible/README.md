# useVisible

Возвращает флаг, указывающий, виден ли компонент в области видимости браузерного окна.

Может принимать 3 значения:

- `true` - элемент виден в области видимости браузера;
- `false` - элемент не виден в области видимости браузера;
- `undefined` - состояние не определено (еще не начали следить за элементом);

## Пример использования

```typescript jsx
import React, { useRef } from 'react';
import { useVisible } from '@yandex-int/tap-components/hooks';

const Component: React.FC = () => {
    const ref = useRef();
    const isVisible = useVisible(ref);

    return <div ref={ref} />;
};
```

## Параметры

```typescript jsx
function useVisible(ref: React.RefObject<HTMLElement>, options: IntersectionObserverInit): boolean;
```

| Свойство | Тип                            | Описание                           |
| -------- | ------------------------------ | ---------------------------------- |
| options? | `IntersectionObserverInit`     | Параметры для IntersectionObserver |
| ref      | `React.RefObject<HTMLElement>` | Ссылка на отслеживаемый элемент    |

## Поддержка

Для работы в старых версиях браузера необходим [полифил](https://github.com/w3c/IntersectionObserver/tree/master/polyfill) для `IntersectionObserver`

Поддержка без полифила:

Safari >= 11 \
Chrome >= 52
