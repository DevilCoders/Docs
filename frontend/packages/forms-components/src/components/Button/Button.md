# Button

<!-- description:start -->
Расширяет Button из `lego-components`.
<!-- description:end -->

## Пример использования

```ts
import React from 'react';
import { compose, composeU } from '@bem-react/core';
import {
  Button as ButtonBase,
  withSizeL,
  withSizeM,
  withSizeS,
  withViewDefault,
} from '@yandex-int/forms-components/Button/desktop';

const Button = compose(
  composeU(withViewDefault),
  composeU(withSizeM, withSizeS, withSizeL),
)(ButtonBase);

const App = () => {
  return (
    <Button size="m" view="default">
      Кнопка
    </Button>
  );
};
```

## Модификаторы

<!-- modifiers:start -->
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/forms-components/src/components/Button)
