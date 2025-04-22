# RatingDynamicStateless

<!-- description:start -->
Компонент для выставления рейтинга без стейта.
<!-- description:end -->

## Примеры

### Пример использования

```ts
import React, { useState } from 'react';
import { RatingDynamicStateless } from '@components/RatingDynamicStateless';

// Использование компонента в вашем приложении
const App = () => {
  const [value, setValue] = useState('');
  return (<RatingDynamicStateless onChange={(value) => setValue(value) />);
};
```

## Свойства

<!-- props:start -->
| Свойство  | Тип                          | Описание                                   |
| --------- | ---------------------------- | ------------------------------------------ |
| value?    | `number`                     | Значение рейтинга от 1 до maxValue.        |
| innerRef? | `RefObject<HTMLSpanElement>` | Ссылка на корневой DOM элемент компонента. |
| size?     | `m \| l`                     | Размер звезд.                              |
| onChange? | `(value?: number) => void`   | Обработчик события изменения рейтинга.     |
<!-- props:end -->
