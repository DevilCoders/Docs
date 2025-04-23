# ReviewEditable

<!-- description:start -->
Компонент оставления отзыва.
<!-- description:end -->

## Примеры

### Пример использования

```ts
import React, { useState } from 'react';
import { ReviewEditable } from '@components/ReviewEditable/desktop';

// Использование компонента в вашем приложении
const App = () => {
  return (
    <ReviewEditable
      author={{ name: 'Инокентий Х.', level: 'Знаток города 5 уровня', url: 'https://yandex.ru',}}
      ratingTitle="Оцените это место",
      ratingTooltipText="Оцените организацию, чтобы опубликовать отзыв." />
  );
};
```

## Свойства

<!-- props:start -->
| Свойство            | Тип                               | Описание                                                   |
| ------------------- | --------------------------------- | ---------------------------------------------------------- |
| author              | `IReviewAuthorProps`              | Данные о пользователе.                                     |
| ratingTitle?        | `string`                          | Тайтл для оставления оценки.                               |
| ratingTooltipText   | `string`                          | Текст в подсказке для выставления оценки.                  |
| rating?             | `number`                          | Оценка пользователя.                                       |
| review?             | `string`                          | Текстовый отзыв пользователя.                              |
| showReviewForm?     | `boolean`                         | Предпоказ формы для оставления текстового отзыва.          |
| popupScope?         | `React.RefObject<HTMLDivElement>` | Ссылка на корневой DOM элемент, в котором размещать попап. |
| onChangeRating?     | `(value?: number) => void`        | Обработчик изменения оценки пользователя.                  |
| onChangeReview?     | `(value?: string) => void`        | Обработчик изменения отзыва пользователя.                  |
| onCancelReviewEdit? | `() => boolean | undefined`       | Обработчик отмены редактирования отзыва.                   |
| objectInfo?         | `IReviewEditableObjectInfoProps`  | Данные про объект на который оставляется отзыв             |
<!-- props:end -->
