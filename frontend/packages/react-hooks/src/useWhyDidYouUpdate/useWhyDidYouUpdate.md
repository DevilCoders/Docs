# useWhyDidYouUpdate

Хук, который выводит в консоль пропсы, изменившиеся с предыдущего рендера.

Помогает найти **возможно** ненужные рендеры.

## Пример

```typescript jsx
import React, { useEffect } from "react";
import { useWhyDidYouUpdate } from "@yandex-int/react-hooks";

const Component = (props) => {
  const changedProps = useWhyDidYouUpdate(props);

  console.log("Измененные пропсы", changedProps);

  return <></>;
};
```

## Параметры

Параметры передаются в виде аргументов функции.

| Свойство | Тип                       | Описание                                                                         |
| -------- | ------------------------- | -------------------------------------------------------------------------------- |
| props    | `Record<string, unknown>` | Пропсы для отслеживания.                                                         |
| isLogged | `false \| true`            | Флаг логирования. <br>Для работы `console.log` должен быть доступен в контексте. |

## Возвращаемое значение

Хук возвращает объект `changedProps`, вида:

```js
{
  propA: {
    from: 'oldValue',
    to: 'newValue'
  },
  propB: {
    from: 'oldValue',
    to: 'newValue'
  }
}
```
