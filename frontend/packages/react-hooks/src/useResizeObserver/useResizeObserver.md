# useResizeObserver

Хук для трекинга изменения ширина/высоты элемента.

**Важно!** Для использования понадобится установить `resize-observer-polyfill`.

## Пример

```typescript jsx
import React from "react";
import { useResizeObserver } from "@yandex-int/react-hooks";

const Component = () => {
  const [ref, width, height] = useResizeObserver<HTMLDivElement>();

  return <div ref={ref} />;
};
```

## Параметры

Нет параметров.

## Возвращаемое значение

Хук возвращает массив.

| Свойство | Тип                   | Описание                   |
| -------- | --------------------- | -------------------------- |
| ref      | `RefObject<TElement>` | Ссылка на DOM-элемент.     |
| width    | `number`              | Текущая ширина компонента. |
| height   | `number`              | Текущая высота компонента. |
