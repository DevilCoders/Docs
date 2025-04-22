# Button

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/Button'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

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
} from '@yandex-int/tools-components/Button/desktop';

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
