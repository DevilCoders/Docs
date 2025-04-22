# MarkerMatching

<!-- description:start -->
Компонент для задач на сопоставление элементов одного списка другому.
<!-- description:end -->

## Примеры

### Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { withRegistry, Registry } from '@bem-react/di';
import {
  cnMarkerMatching,
  MarkerMatching as MarkerMatchingBase,
  withLayoutHorizontal,
} from 'edu-components/MarkerMatching/desktop';
import { List as ListBase, withFlavorBlueberry } from 'edu-components/List/desktop';
// Импортируйте готовый селект или соберите свой
import { Select } from '@yandex-lego/components/Select/desktop/bundle';

// Создаем реестр
const markerMatchingRegistry = new Registry({ id: cnMarkerMatching() });

// Устанавливаем в него собранные элементы
markerMatchingRegistry.set('Select', Select);
markerMatchingRegistry.set('List', withFlavorBlueberry(ListBase));

// Собираем маркер
const MarkerMatching = compose(
  withRegistry(markerMatchingRegistry),
  withLayoutHorizontal,
)(MarkerMatchingBase);

// Используем в приложении
const App = () => (
  <MarkerMatching
    layout="horizontal"
    flavor="blueberry"
    listOfKeys={{
      naming: 'numbers',
      choices: ['1', '2'],
    }}
    listOfValues={{
      naming: 'abcLocal',
      choices: ['A', 'B'],
    }}
    value={{}}
    onChange={e => console.log(e.target.value)}
  />
);
```

## Свойства

<!-- props:start -->
| Свойство     | Тип                                                                                      | По умолчанию | Описание                                                                                                                                 |
| ------------ | ---------------------------------------------------------------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| type?        | `"checkbox" \| "radio"`                                                                  | `'radio'`    | Тип выбора.                                                                                                                              |
| listOfKeys   | `{ naming: TAllowedNaming; choices: ReactNode[]; hidden?: boolean; title?: ReactNode; }` | —            | Объект, описывающий список ключей (то, чему сопоставляют).                                                                               |
| listOfValues | `{ naming: TAllowedNaming; choices: ReactNode[]; hidden?: boolean; title?: ReactNode; }` | —            | Объект, описывающий список значений для сопоставления.                                                                                   |
| value        | `{ [x: string]: string[]; }`                                                             | —            | Текущее значение. Объект, где ключи — индексы элементов левого списка, значения — массив с индексами выбранных элементов правого списка. |
| onChange?    | `(e: { target: { value: Record<string, string[]>; }; }) => void`                         | —            | Обработчик изменения значения маркера.                                                                                                   |
| disabled?    | `false \| true`                                                                          | `false`      | Неактивное состояние. Состояние, при котором компонент выглядит и ведет себя неактивно.                                                  |
| readOnly?    | `false \| true`                                                                          | `false`      | Состояние только для чтения. Состояние, при котором компонент выглядит как обычно, но изменить его значение невозможно.                  |
| statuses?    | `{ [x: string]: TAnswerStatus; }`                                                        | `{}`         | Статусы проверки маркера. Объект, где ключи — индексы элементов списка ключей, значения — статусы проверки.                              |
| flavor?      | `string`                                                                                 | —            | Внешний вид компонента. Передаётся в List.                                                                                               |
| className?   | `string`                                                                                 | —            | Дополнительный класс.                                                                                                                    |
| innerRef?    | `(instance: HTMLDivElement) => void \| RefObject<HTMLDivElement>`                        | —            | Ссылка на корневой DOM-элемент.                                                                                                          |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### layout

Задает расположение списков.

**Допустимые значения:** `"horizontal"`, `"vertical"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerMatching)
- [Описание формата](https://docs.pelican.common.yandex.ru/formats/markers/matching.html)
