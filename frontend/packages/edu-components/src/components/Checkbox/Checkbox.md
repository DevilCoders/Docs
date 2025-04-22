# Checkbox

<!-- description:start -->
Расширяет Checkbox из `lego-components`.
<!-- description:end -->

## Пример использования

```tsx
import React from 'react';
import { compose, composeU } from '@bem-react/core';
import {
  Checkbox as CheckboxBase,
  withSizeM,
  withSizeS,
  withViewLyceum,
  withViewDefault,
  withIndeterminate
} from '@yandex-int/edu-components/Checkbox/desktop';

const Checkbox = compose(
  composeU(withSizeM, withSizeS),
  composeU(withViewDefault, withViewLyceum),
  withIndeterminate
)(CheckboxBase);

const App = () => {
  return <Checkbox checked label="Чекбокс" theme="normal" view="lyceum" size="m" />;
};
```

## Модификаторы

<!-- modifiers:start -->
### view

Задает внешний вид переключателя.

Для `'lyceum'` на сервисе должен быть установлен шрифт "YS Text", например, с помощью пакета [https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/packages/yandex-font](yandex-font).

**Допустимые значения:** `"lyceum"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Checkbox)
