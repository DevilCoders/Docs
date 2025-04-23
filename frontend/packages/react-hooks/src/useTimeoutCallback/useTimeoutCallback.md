# useTimeoutCallback

Хук для вызова функции по истечению таймера.

**Важно!** Функция `setTimeout` должна быть доступна в контексте.

## Пример

```typescript jsx
import React, { useEffect } from "react";
import { useTimeoutCallback } from "@yandex-int/react-hooks";

const Component = () => {
  const [run, cancel] = useTimeoutCallback(() => console.log("Таймер закончился."), 5000);

  useEffect(() => {
    run();
  }, []);

  return <></>;
};
```

## Параметры

Параметры передаются в виде аргументов функции.

| Свойство | Тип                  | Описание                      |
| -------- | -------------------- | ----------------------------- |
| handler  | `TimerHandler`       | Обработчик окончания таймера. |
| timeout  | `number | undefined` | Время до таймаута в мс.       |

## Возвращаемое значение

Хук возвращает массив.

| Свойство | Тип          | Описание                    |
| -------- | ------------ | --------------------------- |
| run      | `() => void` | Функция для старта таймера. |
| cancel   | `() => void` | Функция для отмены таймера. |
