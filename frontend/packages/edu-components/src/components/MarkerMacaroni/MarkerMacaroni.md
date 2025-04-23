# MarkerMacaroni

<!-- description:start -->
Компонент маркера соединения пунктов выбора.
<!-- description:end -->

## Примеры

### Пример использования

```tsx
import React from 'react';
import { withRegistry, Registry } from '@bem-react/di';
import { compose } from '@bem-react/core';

import {
  MarkerMacaroni as MarkerMacaroniBase,
  withFlavorBlueberry,
  withMarkerLine,
  withMarkerList,
  cnMarkerMacaroni,
} from '@yandex-int/edu-components/MarkerMacaroni/desktop';
import {
  Line as LineBase,
  withShapeZ,
  withFlavorBlueberry as withLineFlavorBlueberry,
} from '@yandex-int/edu-components/Line/desktop';
import {
  List as ListBase,
  withFlavorBlueberry as withListFlavorBlueberry,
} from '@yandex-int/edu-components/List';
import {
  Option as OptionBase,
  withFlavorBlueberry as withOptionFlavorBlueberry,
} from '@yandex-int/edu-components/Option/desktop';
import {
  Pin as PinBase,
  withFlavorBlueberry as withPinFlavorBlueberry,
} from '@yandex-int/edu-components/Pin';

// Создаем реестр
const markerMacaroniRegistry = new Registry({ id: cnMarkerMacaroni() });

// Собираем компоненты
const Line = compose(withShapeZ, withLineFlavorBlueberry, withMarkerLine)(LineBase);
const List = compose(withListFlavorBlueberry, withMarkerList)(ListBase);
const Option = compose(withOptionFlavorBlueberry)(OptionBase);
const Pin = compose(withPinFlavorBlueberry)(PinBase);

// Вставляем необходимые реализации компонентов
markerMacaroniRegistry.fill({ Line, List, Option, Pin });

// Соберите компонент с нужным реестром и свойствами
const MarkerMacaroni = compose(
  withRegistry(markerMacaroniRegistry),
  withFlavorBlueberry,
)(MarkerMacaroniBase);

// Используйте в приложении
const App = () => (
  <MarkerMacaroni
    flavor="blueberry"
    lineShape="z"
    value={[]}
    onChange={newValue => console.log(newValue)}
  />
);
```

### Внешний вид

Чтобы изменить внешний вид маркера, используйте модификатор `_flavor`.

#### blueberry

{{%story::desktop:edu-components-markermacaroni-blueberry-desktop--default%}}

## Свойства

<!-- props:start -->
| Свойство          | Тип                                                               | По умолчанию | Описание                                                                                                                |
| ----------------- | ----------------------------------------------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------- |
| innerRef?         | `(instance: HTMLDivElement) => void \| RefObject<HTMLDivElement>` | —            | Ссылка на корневой DOM-элемент.                                                                                         |
| lists             | `{ left: TMarkerList; right: TMarkerList; }`                      | —            | Списки маркера.                                                                                                         |
| flavor?           | `string`                                                          | —            | Внешний вид элементов маркера.                                                                                          |
| lineShape?        | `string`                                                          | —            | Форма линий.                                                                                                            |
| className?        | `string`                                                          | —            | Дополнительный класс.                                                                                                   |
| statuses?         | `TAnswerStatus[]`                                                 | —            | Статусы ответов.                                                                                                        |
| value?            | `TMatch[]`                                                        | `[]`         | Ответы маркера.                                                                                                         |
| onChange?         | `(e: { target: { value: TMatch[]; }; }) => void`                  | —            | Обработчик изменения ответа.                                                                                            |
| pinSize?          | `number`                                                          | `0`          | Размер значка у пункта списка.                                                                                          |
| selectedListItem? | `{ id: number; orientation: TListOrientation; }`                  | —            | Выбранный элемент из списка.                                                                                            |
| hoveredListItem?  | `{ id: number; orientation: TListOrientation; }`                  | —            | Элемент списка над которым находится указатель.                                                                         |
| onMouseMove?      | `(event: MouseEvent<Element, MouseEvent>) => void`                | —            | Обработчик перемещения курсора по маркеру.                                                                              |
| onMouseOver?      | `(event: MouseEvent<Element, MouseEvent>) => void`                | —            | Обработчик наведения курсора на маркер.                                                                                 |
| onMouseOut?       | `(event: MouseEvent<Element, MouseEvent>) => void`                | —            | Обработчик снятия наведения курсора на маркер.                                                                          |
| onMouseDown?      | `(event: MouseEvent<Element, MouseEvent>) => void`                | —            | Обработчик нажатия мыши на маркер.                                                                                      |
| onMouseUp?        | `(event: MouseEvent<Element, MouseEvent>) => void`                | —            | Обработчик снятия нажатия мыши на маркер.                                                                               |
| onTouchMove?      | `(event: TouchEvent<Element>) => void`                            | —            | Обработчик ведения нажатия по маркеру.                                                                                  |
| onTouchCancel?    | `(event: TouchEvent<Element>) => void`                            | —            | Обработчик отмены нажатия.                                                                                              |
| onTouchStart?     | `(event: TouchEvent<Element>) => void`                            | —            | Обработчик тапа на маркер.                                                                                              |
| onTouchEnd?       | `(event: TouchEvent<Element>) => void`                            | —            | Обработчик снятия тапа со маркера.                                                                                      |
| onItemSelected?   | `(selectedId: number) => boolean`                                 | —            | Обработчик выбора элемента списка.<br>Возвращает `false`, если создавать линию не нужно.                                |
| disabled?         | `false \| true`                                                   | `false`      | Неактивное состояние. Состояние, при котором компонент выглядит и ведет себя неактивно.                                 |
| readOnly?         | `false \| true`                                                   | `false`      | Состояние только для чтения. Состояние, при котором компонент выглядит как обычно, но изменить его значение невозможно. |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### flavor

Задает внешний вид маркера.

Для модификаторов выставляются значения `pinSize` по-умолчанию:

-   Для `blueberry` значение равно `12`
-   Для `grape` значение равно `8`

**Допустимые значения:** `"blueberry"`, `"grape"`.
<!-- modifiers:end -->

## Универсальная платформа

В компоненте есть реализация для универсальной платформы.

Универсальная (`universal`) – это платформа, объединяющая `desktop` и `touch` платформы. В компоненте есть обработчики событий как для мыши, так и для тачей. Примерами устройств, для которых может понадобится универсальный компонент являются: маркерные доски, компьютеры с сенсорными экранами.

Пример импорта компонента:
```typescript jsx
import { MarkerMacaroni } from '@yandex-int/edu-components/MarkerMacaroni/universal';
```

Обычно элементы компонента исключают стили для `hover` и фокус при табуляции для `common` и `touch` версий, поэтому следует импортировать десктопные версии для сбора компонентов.

Например, для `MarkerMacaroni`, нужно импортировать `desktop` версию атома `Option`:
```typescript jsx
import { Option } from '@yandex-int/edu-components/Option/desktop';
```

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerMacaroni)
- [Описание формата](https://docs.pelican.common.yandex.ru/formats/markers/macaroni.html)
