# Icon

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/Icon'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

Расширяет Icon из `lego-components`.

## Пример подключения

Использование с нужным набором модификаторов:

```ts
import React from 'react';
import { compose } from '@bem-react/core';
import {
  Icon as IconDesktop,
  withTypeError,
} from '@yandex-int/tools-components/Icon/desktop'

const Icon = compose(
  withTypeError,
)(IconDesktop);

const App = () => {
  return (
    <Icon type="error"/>
  );
};
```

## Примеры

### Тип

С помощью свойства `type`:

{{%story::desktop:tools-components-icon-desktop--type%}}

