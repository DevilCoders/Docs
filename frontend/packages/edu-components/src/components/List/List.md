# List

<!-- description:start -->
Компонент списка.
<!-- description:end -->

## Примеры

### Пример использования

```tsx
import React from 'react';
import { compose } from '@bem-react/di';
import { withRegistry, Registry } from '@bem-react/di';
import { List as ListBase, cnList } from '@yandex-int/edu-components/List/desktop';
import { Option } from '@yandex-int/edu-components/Option/desktop';

const listRegistry = new Registry({ id: cnList() });
listRegistry.set('Option', Option);

const List = withRegistry(listRegistry)(ListBase);

const options = ['Option 1', 'Option 2'];

const App = () => (
  <List options={options} />;
);
```

## Свойства

<!-- props:start -->
| Свойство            | Тип                                                                                                                                                                                                                                                               | По умолчанию | Описание                                  |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ----------------------------------------- |
| className?          | `string`                                                                                                                                                                                                                                                          | —            | Дополнительный класс.                     |
| listItemsClassName? | `string`                                                                                                                                                                                                                                                          | —            | Дополнительный класс для List-Items.      |
| naming?             | `"abc" \| "abcLower" \| "abcLocal" \| "abcLocalLower" \| "numbers"`                                                                                                                                                                                               | —            | Тип именования индексов пунктов списка.   |
| innerRef?           | `RefObject<HTMLElement>`                                                                                                                                                                                                                                          | —            | Ссылка на DOM элемент списка.             |
| options?            | `ReactNode[]`                                                                                                                                                                                                                                                     | `[]`         | Контент пунктов списка.                   |
| title?              | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —            | Заголовок списка.                         |
| renderListItem?     | `(listItem: TListItem) => ReactNode`                                                                                                                                                                                                                              | —            | Функция для отображения элементов списка. |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### flavor

Отвечает за внешний вид элементов списка.

**Допустимые значения:** `"blueberry"`, `"grape"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/List)
