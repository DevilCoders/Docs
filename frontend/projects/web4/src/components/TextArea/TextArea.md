# TextArea

<!-- description:start -->
Многострочное текстовое поле.
<!-- description:end -->

## Примеры

### Пример использования

```ts
import React, { useState } from 'react';
import { TextArea } from '@components/TextArea/desktop';

// Использование компонента в вашем приложении
const App = () => {
  const [value, setValue] = useState('');
  return (
    <Textarea
      placeholder="Тестовый плейсхолдер"
      theme="normal"
      view="classic"
      size="s"
      maxLength={20000}
      rows={5}
      value={value}
      onChange={(event) => setValue(event.target.value)}
      hasClear
    />
  );
};
```

## Ссылки

- [Подробнее в lego-components](https://gitlab.yandex-team.ru/search-interfaces/frontend/blob/master/packages/lego-components/src/components/Textarea/Textarea.md)
