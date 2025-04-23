# useComponentContext

Хук для использования именованного контекста компонента.

## Пример

```typescript jsx
import React from "react";
import { useComponentContext } from "@yandex-int/react-hooks";

const ParentComponentContext = createContext({} as { text: string });

const useParentContext = (childComponentName: string) => {
  return useComponentContext(ParentComponentContext, ".ParentComponent", childComponentName);
};

const ChildComponent = () => {
  const { text } = useParentContext(".ChildComponent");

  return <>Дочерний компонент и контекст: {text}</>;
};
```

## Параметры

Параметры передаются в виде аргументов функции.

| Свойство         | Тип               | Описание                           |
| ---------------- | ----------------- | ---------------------------------- |
| ComponentContext | `Context<TValue>` | Контекст родительского компонента. |
| componentName    | `string`          | Имя родительского компонента.      |
| childName        | `string`          | Имя дочернего компонента.          |

## Возвращаемое значение

Хук возвращает контекст родительского компонента.
