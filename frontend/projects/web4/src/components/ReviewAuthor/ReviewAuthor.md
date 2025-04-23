# ReviewAuthor

<!-- description:start -->
Компонент информации о пользователе, оставившем отзыв.
<!-- description:end -->

## Примеры

### Пример использования

```ts
import React, { useState } from 'react';
import { ReviewAuthor } from '@components/ReviewAuthor/ReviewAuthor@desktop';

const App = () => {
  return (
    <ReviewAuthor
      name="Инокентий Х."
      level="Знаток города 5 уровня"
      url="https://yandex.ru"
    />
  );
};
```

## Свойства

<!-- props:start -->
| Свойство  | Тип      | Описание                            |
| --------- | -------- | ----------------------------------- |
| name      | `string` | Имя пользователя.                   |
| avatarId? | `string` | ID аватарки пользователя.           |
| url?      | `string` | Ссылка на публичный личный кабинет. |
| level?    | `string` | Уровень пользователя.               |
<!-- props:end -->
