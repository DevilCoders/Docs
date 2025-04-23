# useStaffCard

Хук для подключения staff карточки.

**Поддерживает YandexTeam и сервисы Коннекта в B2B.**

## Пример

```typescript jsx
import React, { useRef } from "react";
import { useStaffCard } from "@yandex-int/react-hooks";

const Component = () => {
  const anchorRef = useRef(null);

  useStaffCard({
    anchorRef,
    login: "robot-startrek",
  });

  return <div ref={anchorRef} />;
};
```

## Параметры

```typescript
type UseStaffCardProps = {
  /**
   * Элемент к которому подключается карточка
   */
  anchorRef: RefObject<HTMLElement | undefined>;

  /**
   * Логин пользователя
   */
  login: string;

  /**
   * Окружение пользователя
   */
  env?: "yateam" | "b2b";

  /**
   * Uid пользователя - Обязателен для работы B2B
   */
  uid?: string;

  /**
   * Название сервиса - Обязателен для работы B2B
   */
  from?: string;

  /**
   * Хост стаффа - Обязателен для работы B2B
   */
  staffOrigin?: string;
};
```

## Возвращаемое значение

Хук ничего не возвращает.

## Мок карточки в Hermione

Добавить в начало страницы скрипт.

```js
class StaffCard {
  destruct() {}
}
```
