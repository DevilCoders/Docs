# Line

<!-- description:start -->
Компонент линии.
<!-- description:end -->

Вне родительского тега `svg` компонент не имеет смысла.

Может являться частью `MarkerMacaroni`.

## Примеры

### Пример использования

```typescript jsx
import React from 'react';
import { compose } from '@bem-react/core';
import { Line as LineBase, withFlavorBlueberry, withShapeZ } from '@yandex-int/edu-components/Line/desktop';

const Line = compose(
  withShapeZ,
  withFlavorBlueberry,
)(LineBase);

const start = {
  x: 10,
  y: 10,
};

const end = {
  x: 110,
  y: 110,
};

const App = () => (
  <svg>
    <Line start={start} end={end} flavor="blueberry" shape="z" />
  </svg>
);
```

### Внешний вид

Чтобы изменить внешний вид компонента, используйте модификатор `_flavor`.

#### blueberry

{{%story::desktop:edu-components-line-blueberry--states%}}

### Форма линии

Чтобы изменить форму линии, используйте модификатор `_shape`.

#### z

{{%story::desktop:edu-components-line-shapes--z%}}

#### straight

{{%story::desktop:edu-components-line-shapes--straight%}}

## Свойства

<!-- props:start -->
| Свойство   | Тип                                                         | Описание                                              |
| ---------- | ----------------------------------------------------------- | ----------------------------------------------------- |
| start?     | `{ x: number; y: number; }`                                 | Координаты начала линии.                              |
| end?       | `{ x: number; y: number; }`                                 | Координаты конца линии.                               |
| progress?  | `false \| true`                                             | Флаг "В процессе создания линии".                     |
| linePath?  | `string`                                                    | Строка с SVG командами для отрисовки линии.           |
| className? | `string`                                                    | Дополнительный класс.                                 |
| innerRef?  | `(instance: SVGGElement) => void \| RefObject<SVGGElement>` | Ссылка на корневой DOM-элемент.                       |
| disabled?  | `false \| true`                                             | Можно ли взаимодействовать с линией.                  |
| readOnly?  | `false \| true`                                             | Режим чтения.<br>В этом режиме линию нельзя изменять. |
| onClick?   | `(event: MouseEvent<SVGGElement, MouseEvent>) => void`      | Обработчик клика на линию.                            |
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
### flavor

Задает внешний вид линии.

**Допустимые значения:** `"blueberry"`, `"grape"`.

### shape

Задает форму линии.

**Допустимые значения:** `"straight"`, `"z"`.
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Line)
