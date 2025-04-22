# RatingDynamic

<!-- description:start -->
Компонент для выставления рейтинга.
<!-- description:end -->

## Примеры

### Пример использования

```ts
import React, { useState } from 'react';
import { RatingDynamic } from '@components/RatingDynamic';

// Использование компонента в вашем приложении
const App = () => {
  const [value, setValue] = useState('');
  return (<RatingDynamic onChange={(value) => setValue(value) />);
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
