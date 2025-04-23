# MarkerSeparator

<!-- description:start -->
Компонент для view маркера разделителя.
Разделители переключаются циклически в порядке, заданном `options`.
<!-- description:end -->

## Примеры

### Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import {
  MarkerSeparator as MarkerSeparatorBase,
  withCurrentPlaceholder,
  withCurrentHyphen,
  withCurrentSeparate,
  withCurrentTogether,
  withFlavorBlueberry,
} from '@yandex-int/edu-components/MarkerSeparator/desktop';

const MarkerSeparator = compose(
  withCurrentPlaceholder,
  withCurrentHyphen,
  withCurrentSeparate,
  withCurrentTogether,
  withFlavorBlueberry,
)(MarkerSeparatorBase);

const App = () => (
  <MarkerSeparator
    id="input-unique-id"
    flavor="blueberry"
    options={['hyphen', 'separate', 'together']}
    status="correct"
    value={0}
    onChange={e => console.log(e.target.value)}
  />
);
```

### Разделитель запятая
{{%story::desktop:edu-components-markerseparator--comma%}}

### Внешний вид

Чтобы изменить внешний вид маркера, используйте модификатор `_flavor`.

{{%story::desktop:edu-components-markerseparator--flavors%}}

## Свойства

<!-- props:start -->
| Свойство     | Тип                                                                 | По умолчанию | Описание                                                                                                                |
| ------------ | ------------------------------------------------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------- |
| id           | `string`                                                            | —            | Уникальный идентификатор.                                                                                               |
| highlighted? | `false \| true`                                                     | `true`       | Визуально выделяет маркер.                                                                                              |
| options      | `string[]`                                                          | —            | Массив значений, между которыми происходит переключение.                                                                |
| value?       | `number`                                                            | `null`       | Значение маркера – индекс значения в массиве. Не передавайте численное значение, чтобы отобразить плейсхолдер '?'.      |
| onChange     | `(e: { target: { value: number; }; }) => void`                      | —            | Обработчик, срабатывающий на переключение и передающий новое значение.                                                  |
| disabled?    | `false \| true`                                                     | `false`      | Неактивное состояние. Состояние, при котором компонент выглядит и ведет себя неактивно.                                 |
| readOnly?    | `false \| true`                                                     | `false`      | Состояние только для чтения. Состояние, при котором компонент выглядит как обычно, но изменить его значение невозможно. |
| status?      | `"initial" \| "correct" \| "incorrect" \| "accepted"`               | `'initial'`  | Статус маркера.                                                                                                         |
| innerRef?    | `(instance: HTMLSpanElement) => void \| RefObject<HTMLSpanElement>` | —            | Ссылка на корневой DOM-элемент компонента.                                                                              |
| className?   | `string`                                                            | —            | Дополнительный className.                                                                                               |
<!-- props:end -->

## Модификаторы

### current

Внутренний модификатор с текущим выбранным разделителем.

Его нельзя задать явно: значение зависит от переданного `value`.
Если `value` не передан или `null`, в `_current` попадает плейсхолдер.

<!-- modifiers:start -->
### flavor

Задает внешний вид маркера.

**Допустимые значения:** `"blueberry"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerSeparator)
- [Описание формата](https://docs.pelican.common.yandex.ru/formats/markers/inline.html)
