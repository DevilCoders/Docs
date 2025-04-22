# Pin

<!-- description:start -->
Компонент значка.
<!-- description:end -->

Может являться частью `List`.

## Примеры

### Пример использования

```tsx
import React from 'react';
import { compose } from '@bem-react/core';
import {
  Pin as PinBase,
  withFlavorBlueberry,
} from '@yandex-int/edu-components/Pin/desktop';

const Pin = compose(withFlavorBlueberry)(PinBase);

const App = () => (
  <Pin flavor="blueberry" />
);
```

### Внешний вид

Чтобы изменить внешний вид компонента, используйте модификатор `_flavor`.

#### blueberry

{{%story::desktop:edu-components-pin-blueberry--default%}}

## Свойства

<!-- props:start -->
| Свойство   | Тип                          | Описание                        |
| ---------- | ---------------------------- | ------------------------------- |
| className? | `string`                     | Дополнительный класс.           |
| innerRef?  | `RefObject<HTMLSpanElement>` | Ссылка на корневой DOM-элемент. |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### flavor

Задает внешний вид значка.

**Допустимые значения:** `"blueberry"`, `"grape"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Pin)
