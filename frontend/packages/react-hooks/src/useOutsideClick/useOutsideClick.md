# useOutsideClick

Хук, который вызывает коллбэк на нажатие за пределами элемента из рефа.

Хук поддерживает платформенные версии:

- `common` - событие `click`
- `desktop` - событие `mousedown`
- `touch` - событие `touchstart`

## Пример

```typescript jsx
import React from "react";
// useOutsideClick, useOutsideClickDesktop или useOutsideClickTouch
import { useOutsideClick } from "@yandex-int/react-hooks";

const App = () => {
  const ref = useRef<HTMLDivElement>(null);

  useOutsideClick(ref, () => {
    console.log("Коллбек");
  });

  return <div ref={ref}>Тестовый компонент</div>;
};
```

## Параметры

Параметры передаются в виде аргументов функции.

| Свойство | Тип                                        | Описание                                 |
| -------- | ------------------------------------------ | ---------------------------------------- |
| ref      | `RefObject<Element>`                       | Ссылка на отслеживаемый элемент.         |
| onClick  | `(event: MouseEvent | TouchEvent) => void` | Обработчик события нажатия вне элемента. |

## Возвращаемое значение

Хук не возвращает значений.
