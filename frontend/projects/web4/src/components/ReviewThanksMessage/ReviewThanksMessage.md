# ReviewThanksMessage

<!-- description:start -->
Компонент спасибо. Показывается после оставления отзыва.
<!-- description:end -->

## Примеры

### Пример использования

```ts
import React, { useState } from 'react';
import { ReviewThanksMessage } from '@components/ReviewThanksMessage/desktop';

// Использование компонента в вашем приложении
const App = () => {
  return (
    <ReviewThanksMessage url="https://yandex.ru" onClickClose={onClickClose} />
  );
};
```

## Свойства

<!-- props:start -->
| Свойство     | Тип          | Описание                                |
| ------------ | ------------ | --------------------------------------- |
| url          | `string`     | Ссылка на личный кабинет пользователя.  |
| onClickClose | `() => void` | Обработчик закрытия компонента спасибо. |
<!-- props:end -->
