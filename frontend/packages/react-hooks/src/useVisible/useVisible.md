# useVisible

Хук для определения нахождения компонента в области видимости браузерного окна.

**Важно!** В тестах и примерах для поддержки ie11 используется полифилл `intersection-observer`. Без него хук в данном браузере работать не будет.

## Пример использования

```typescript jsx
import React, { FC, useRef } from "react";
import { useVisible } from "@yandex-int/react-hooks";

const Component: FC = () => {
  const ref = useRef(null);
  const isVisible = useVisible(ref);

  return <div ref={ref} />;
};
```

## Параметры

Параметры передаются в виде аргументов функции.

```typescript jsx
function useVisible(ref: React.RefObject<HTMLElement>, options: IntersectionObserverInit): boolean;
```

| Свойство | Тип                            | Описание                            |
| -------- | ------------------------------ | ----------------------------------- |
| ref      | `React.RefObject<HTMLElement>` | Ссылка на отслеживаемый элемент.    |
| options? | `IntersectionObserverInit`     | Параметры для IntersectionObserver. |

## Возвращаемое значение

Хук возвращает примитив.

Может принимать 3 значения:

- `true` - элемент виден в области видимости браузера;
- `false` - элемент не виден в области видимости браузера;
- `undefined` - состояние не определено (еще не начали следить за элементом);

| Свойство  | Тип       | Описание                 |
| --------- | --------- | ------------------------ |
| isVisible | `false \| true \| undefined` | Флаг видимости элемента. |
