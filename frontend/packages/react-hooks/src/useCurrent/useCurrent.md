# useCurrent

Хук для сохранения текущего значения.

Эти значения могут использованы `unmount`, таким образом обходится механизм замыкания.

## Пример

```typescript jsx
import React from "react";
import { useCurrent } from "@yandex-int/react-hooks";

const Component = (someProp) => {
  useCurrent(someProp, (savedValue) => {
    // cleanup callback on useEffect
    // do something with savedValue
  });

  // or

  const somePropRef = useCurrent(someProp);

  useEffect(() => {
    const sendLastCounter = () => {
      if (somePropRef.current) {
        // do something with savedValue
      }
    };

    window.addEventListener("beforeunload", sendLastCounter);

    return () => {
      window.addEventListener("beforeunload", sendLastCounter);
    };
  }, []);

  return <></>;
};
```

## Параметры

Параметры передаются в виде аргументов функции.

| Свойство | Тип                                   | Описание                         |
| -------- | ------------------------------------- | -------------------------------- |
| value    | `T`                                   | Значение для сохранения.         |
| cb       | `(savedValue: T) => void | undefined` | Функция для вызова на `unmount`. |

## Возвращаемое значение

Хук возвращает объект.

| Свойство | Тип      | Описание                        |
| -------- | -------- | ------------------------------- |
| valueRef | `Ref<T>` | Ссылка с сохраненным значением. |
