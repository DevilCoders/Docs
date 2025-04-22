# useBooleanState

Хук для трекания boolean при помощи useState.

## Пример

```typescript jsx
import React from "react";
import { useBooleanState } from "@yandex-int/react-hooks";

const TestComponent = () => {
  const { state, toggle, setTrue, setFalse } = useBooleanState(false);

  return (
    <div>
      <button onClick={toggle}>Toggle</button>&nbsp;
      <button onClick={setTrue}>Set True</button>&nbsp;
      <button onClick={setFalse}>Set False</button>
      <p>Сейчас значение: {state ? "true" : "false"}</p>
    </div>
  );
};
```

## Параметры

Параметры передаются в виде аргументов функции.

| Свойство     | Тип       | Описание            |
| ------------ | --------- | ------------------- |
| initialState | `boolean` | Начальное значение. |

## Возвращаемое значение

Хук возвращает объект.

| Свойство | Тип                        | Описание                                                |
| -------- | -------------------------- | ------------------------------------------------------- |
| state    | `boolean`                  | Значение текущего состояния.                            |
| setState | `(state: boolean) => void` | Функция для установки текущего значения.                |
| setTrue  | `() => void`               | Функция для установки значения `true`.                  |
| setFalse | `() => void`               | Функция для установки значения `false`.                 |
| toggle   | `() => void`               | Функция для смены значения на противоположный текущему. |
