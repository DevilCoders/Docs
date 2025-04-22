# CoordinateSystem

<!-- description:start -->
Компонент системы координат.
Используйте внутри компонента Svg.
<!-- description:end -->

Относится к универсальной платформе.

## Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemGrid as Grid,
  CoordinateSystemAxes as Axes,
  CoordinateSystemXAxis as XAxis,
  CoordinateSystemYAxis as YAxis,
  CoordinateSystemFnGraph as FnGraph,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <Grid />
      <Axes>
        <XAxis step={2} />
        <YAxis step={2} />
      </Axes>
      <FnGraph fn="sin(e^x)" color="steelblue" />
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem--playground%}}

## Свойства

<!-- props:start -->
| Свойство   | Тип                | Описание                      |
| ---------- | ------------------ | ----------------------------- |
| xDomain    | `[number, number]` | Диапазон значений по оси `x`. |
| yDomain    | `[number, number]` | Диапазон значений по оси `y`. |
| className? | `string`           | Дополнительный класс.         |
<!-- props:end -->

## Хуки

### useCoordinateSystemContext

Позволяет получить доступ к контексту системы координат.

```typescript
import { useCoordinateSystemContext } from '@yandex-int/edu-components/CoordinateSystem/universal';

const { x0, y0, xDomain, yDomain, xScale, yScale } = useCoordinateSystemContext('myComponentName');
```

### useClosestPoint

Находит ближайшую к указателю точку по заданному шагу.

```typescript
import { useClosestPoint } from '@yandex-int/edu-components/CoordinateSystem/universal';

const [closestPoint, setPointerPosition] = useClosestPoint(0.1);
```

### useMovingPoint

Находит точку, соответствующую положению движущегося указателя, по заданному шагу.

```typescript
import { useMovingPoint } from '@yandex-int/edu-components/CoordinateSystem/universal';

const movingPoint = useMovingPoint(0.1);
```

## Компоненты

### Axes

Компонент построения осей.
Если в дочерние оси не переданы отметки, то формирует их с заданным для них шагом.
Убирает крайние отметки и добавляет смещенное общее начало координат.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemAxes as Axes,
  CoordinateSystemXAxis as XAxis,
  CoordinateSystemYAxis as YAxis,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 30 }}>
    <CoordinateSystem xDomain={[0, 1]} yDomain={[0, 1]}>
      <Axes tickSize={4} arrowHeadSize={6} color="#444">
        <XAxis step={0.1} unlabeledTicks={[0.1, 0.3, 0.5, 0.7, 0.9]} />
        <YAxis step={0.1} unlabeledTicks={[0.1, 0.3, 0.5, 0.7, 0.9]} />
      </Axes>
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem-axes--two-axes%}}

#### Свойства

| Свойство       | Тип                                                                                                                                                                                                            | По умолчанию   | Описание                    |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | --------------------------- |
| tickSize?      | `number`                                                                                                                                                                                                       | `4`            | Размер отметок на оси.      |
| arrowHeadSize? | `number`                                                                                                                                                                                                       | `5`            | Размер наконечника стрелки. |
| color?         | `string`                                                                                                                                                                                                       | `currentColor` | Цвет оси.                   |
| children       | `ReactElement<TAxisProps, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| TAxisElement[]` | —              | Дочерние оси.               |
| className?     | `string`                                                                                                                                                                                                       | —              | Дополнительный класс.       |

### XAxis

Компонент горизонтальной оси.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemXAxis as XAxis,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={25} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[0, 10]} yDomain={[0, 1]}>
      <XAxis label="fibonacci" arrowHeadSize={5} ticks={[1, 2, 3, 5, 8]} />
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem-axes--x-axis-with-label%}}

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemXAxis as XAxis,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={25} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-10, 10]} yDomain={[0, 1]}>
      <XAxis label="" tickSize={4} />
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem-axes--x-axis-without-label%}}

#### Свойства

| Свойство        | Тип        | По умолчанию   | Описание                                   |
| --------------- | ---------- | -------------- | ------------------------------------------ |
| label?          | `string`   | `x`            | Подпись оси.                               |
| color?          | `string`   | `currentColor` | Цвет оси.                                  |
| ticks?          | `number[]` | —              | Отметки на оси. Имеют приоритет над шагом. |
| tickSize?       | `number`   | `0`            | Размер отметок.                            |
| unlabeledTicks? | `number[]` | `[]`           | Отметки без подписи.                       |
| step?           | `number`   | `1`            | Шаг для построения отметок.                |
| arrowHeadSize?  | `number`   | `0`            | Размер наконечника стрелки.                |
| className?      | `string`   | —              | Дополнительный класс.                      |

### YAxis

Компонент вертикальной оси.

#### Пример использования

```typescript jsx
import React from 'react';
import { range } from 'd3-array';
import {
  CoordinateSystem,
  CoordinateSystemYAxis as YAxis,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[0, 10]} yDomain={[0, 10]}>
      <YAxis label="скорость, км/ч" tickSize={5} arrowHeadSize={5} ticks={range(1, 10)} />
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem-axes--y-axis-with-label%}}

#### Свойства

| Свойство        | Тип        | По умолчанию   | Описание                                   |
| --------------- | ---------- | -------------- | ------------------------------------------ |
| label?          | `string`   | `y`            | Подпись оси.                               |
| color?          | `string`   | `currentColor` | Цвет оси.                                  |
| ticks?          | `number[]` | —              | Отметки на оси. Имеют приоритет над шагом. |
| tickSize?       | `number`   | `0`            | Размер отметок.                            |
| unlabeledTicks? | `number[]` | `[]`           | Отметки без подписи.                       |
| step?           | `number`   | `1`            | Шаг для построения отметок.                |
| arrowHeadSize?  | `number`   | `0`            | Размер наконечника стрелки.                |
| className?      | `string`   | —              | Дополнительный класс.                      |

### Grid

Компонент построения сетки.
Отметки, через которые будут проходить линии сетки, можно указать явно или задать шаг построения сетки.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemGrid as Grid,
  CoordinateSystemXAxis as XAxis,
  CoordinateSystemYAxis as YAxis,
  CoordinateSystemAxes as Axes,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 30 }}>
    <CoordinateSystem xDomain={[0, 1]} yDomain={[0, 1]}>
      <Grid step={0.1} />
      <Axes>
        <XAxis step={0.1} unlabeledTicks={[0.1, 0.3, 0.5, 0.7, 0.9]} />
        <YAxis step={0.1} unlabeledTicks={[0.1, 0.3, 0.5, 0.7, 0.9]} />
      </Axes>
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem-grids--auto-grid%}}

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemGrid as Grid,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <Grid color="red" xTicks={[-2, -1, 1, 2]} yTicks={[-2, -1, 1, 2]} />
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem-grids--predefined-grid%}}

#### Свойства

| Свойство   | Тип        | По умолчанию   | Описание                                       |
| ---------- | ---------- | -------------- | ---------------------------------------------- |
| xTicks?    | `number[]` | —              | Отметки по оси `x`. Имеют приоритет над шагом. |
| yTicks?    | `number[]` | —              | Отметки по оси `y`. Имеют приоритет над шагом. |
| step?      | `number`   | `1`            | Шаг сетки.                                     |
| color?     | `string`   | `currentColor` | Цвет сетки.                                    |
| className? | `string`   | —              | Дополнительный класс.                          |

### FnGraph

Компонент графика функции. Задается выражением `y` относительно `x`.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemFnGraph as FnGraph,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg>
    <CoordinateSystem>
      <FnGraph fn={'ax + b'} scope={{ a: 10, b: 5 }} color="red">
        <text>annotation</text>
      </FnGraph>
    </CoordinateSystem>
  </Svg>
);
```

#### Примеры графиков

{{%story::edu-components-coordinatesystem--fn-graphs%}}

#### Свойства

| Свойство   | Тип                            | По умолчанию   | Описание                                                                                                                                              |
| ---------- | ------------------------------ | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| fn         | `string`                       | —              | Выражение, задающее функцию. [Описание синтаксиса](https://mathjs.org/docs/expressions/syntax.html). Примеры: "1/x^2", "sin(e^x)", "nthRoot(x, 3)^2". |
| scope?     | `{ [param: string]: number; }` | —              | Параметры функции. Для "kx + b" передайте { k, b }.                                                                                                   |
| precision? | `number`                       | `10`           | Количество вычисляемых значений на единицу ширины.                                                                                                    |
| color?     | `string`                       | `currentColor` | Цвет линии.                                                                                                                                           |
| width?     | `string \| number`             | `2`            | Толщина линии.                                                                                                                                        |
| className? | `string`                       | —              | Дополнительный класс.                                                                                                                                 |

### Point

Компонент точки.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemGrid as Grid,
  CoordinateSystemAxes as Axes,
  CoordinateSystemXAxis as XAxis,
  CoordinateSystemYAxis as YAxis,
  CoordinateSystemPoint as Point,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={200} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-5, 5]} yDomain={[0, 5]}>
      <Grid />
      <Axes>
        <XAxis />
        <YAxis />
      </Axes>

      <Point empty x={0} y={0} color="green" />
      <Point x={2} y={2} color="red" />
      <Point x={-1} y={4} color="orange" size={6} />
    </CoordinateSystem>
  </Svg>
);
```

{{%story::edu-components-coordinatesystem-points--points%}}

#### Свойства

| Свойство   | Тип             | По умолчанию   | Описание                           |
| ---------- | --------------- | -------------- | ---------------------------------- |
| x          | `number`        | —              | Координата по оси `x`.             |
| y          | `number`        | —              | Координата по оси `y`.             |
| size?      | `number`        | `12`           | Размер точки в пикселях (диаметр). |
| color?     | `string`        | `currentColor` | Цвет точки.                        |
| empty?     | `false \| true` | `false`        | Выколотость.                       |
| className? | `string`        | —              | Дополнительный класс.              |

#### Модификаторы

##### draggable

Модификатор, отвечающий за перемещение точки.

| Свойство   | Тип                                            | По умолчанию | Описание                             |
| ---------- | ---------------------------------------------- | ------------ | ------------------------------------ |
| draggable? | `false \| true`                                | —            | Перемещаемость точки.                |
| step?      | `number`                                       | `0.1`        | Шаг построения.                      |
| onChange?  | `(oldPoint: TPoint, newPoint: TPoint) => void` | —            | Колбэк на изменение положения точки. |

### Projection

Компонент проекции точки на оси.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemProjection as Projection,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <Projection annotated x={1} y={2} />
    </CoordinateSystem>
  </Svg>
);
```

#### Свойства

| Свойство   | Тип             | По умолчанию   | Описание                     |
| ---------- | --------------- | -------------- | ---------------------------- |
| x          | `number`        | —              | Координата точки по оси `x`. |
| y          | `number`        | —              | Координата по оси `y`.       |
| width?     | `number`        | `2`            | Толщина линий.               |
| color?     | `string`        | `currentColor` | Цвет линий.                  |
| annotated? | `false \| true` | `false`        | Добавлять ли подписи.        |
| className? | `string`        | —              | Дополнительный класс.        |

### PointSelector

Компонент выбора точки.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemPointSelector as PointSelector,
  CoordinateSystemProjection as Projection,
  CoordinateSystemPoint as Point,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <PointSelector onSelect={point => console.log(`(${point.x}, ${point.y})`)}>
        {({ x, y }) => (
          <>
            <Projection annotated x={x} y={y} />
            <Point x={x} y={y} size={6} />
          </>
        )}
      </PointSelector>
    </CoordinateSystem>
  </Svg>
);
```

#### Свойства

| Свойство | Тип                                   | По умолчанию | Описание                            |
| -------- | ------------------------------------- | ------------ | ----------------------------------- |
| step?    | `number`                              | `0.1`        | Шаг построения.                     |
| children | `(currentPoint: TPoint) => ReactNode` | —            | Функция рендера точки.              |
| onSelect | `(selectedPoint: TPoint) => void`     | —            | Функция, вызываемая на выбор точки. |

### Line

Компонент прямой.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemLine as Line,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <Line
        points={[
          { x: 1, y: 2 },
          { x: 2, y: 3 },
        ]}
      />
    </CoordinateSystem>
  </Svg>
);
```

#### Свойства

| Свойство   | Тип                           | По умолчанию   | Описание                    |
| ---------- | ----------------------------- | -------------- | --------------------------- |
| points     | `{ x: number; y: number; }[]` | —              | Две точки, задающие прямую. |
| color?     | `string`                      | `currentColor` | Цвет линии.                 |
| width?     | `number`                      | `2`            | Толщина линии.              |
| className? | `string`                      | —              | Дополнительный класс.       |

### LineSegment

Компонент отрезка.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemLineSegment as LineSegment,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <LineSegment
        points={[
          { x: 1, y: 2 },
          { x: 2, y: 3 },
        ]}
      />
    </CoordinateSystem>
  </Svg>
);
```

#### Свойства

| Свойство   | Тип                           | По умолчанию   | Описание                     |
| ---------- | ----------------------------- | -------------- | ---------------------------- |
| points     | `{ x: number; y: number; }[]` | —              | Две точки, задающие отрезок. |
| color?     | `string`                      | `currentColor` | Цвет линии.                  |
| width?     | `number`                      | `2`            | Толщина линии.               |
| className? | `string`                      | —              | Дополнительный класс.        |

### Ray

Компонент луча.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemRay as Ray,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <Ray
        points={[
          { x: 1, y: 2 },
          { x: 2, y: 3 },
        ]}
      />
    </CoordinateSystem>
  </Svg>
);
```

#### Свойства

| Свойство   | Тип                           | По умолчанию   | Описание                                                   |
| ---------- | ----------------------------- | -------------- | ---------------------------------------------------------- |
| points     | `{ x: number; y: number; }[]` | —              | Две точки, задающие луч. Первая точка считается начальной. |
| color?     | `string`                      | `currentColor` | Цвет линии.                                                |
| width?     | `number`                      | `2`            | Толщина линии.                                             |
| className? | `string`                      | —              | Дополнительный класс.                                      |

### Polygon

Компонент многоугольника.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemPolygon as Polygon,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <Polygon
        points={[
          { x: 1, y: 2 },
          { x: 2, y: 3 },
          { x: 5, y: 10 },
        ]}
        color="rgba(255,0,0,0.24)"
      />
    </CoordinateSystem>
  </Svg>
);
```

#### Свойства

| Свойство      | Тип          | По умолчанию   | Описание                     |
| ------------- | ------------ | -------------- | ---------------------------- |
| points        | `TPoint[]`   | —              | Набор вершин многоугольника. |
| color?        | `string`     | `currentColor` | Цвет многоугольника.         |
| outlineColor? | `string`     | `transparent`  | Цвет обводки.                |
| outlineWidth? | `number`     | `1`            | Ширина обводки.              |
| className?    | `string`     | —              | Дополнительный класс.        |
| onClick?      | `() => void` | —              | Обработчик клика.            |

### Hull

Компонент выпуклой оболочки.

#### Пример использования

```typescript jsx
import React from 'react';
import {
  CoordinateSystem,
  CoordinateSystemHull as Hull,
} from '@yandex-int/edu-components/CoordinateSystem/universal';
import { Svg } from '@yandex-int/edu-components/Svg/universal';

const App = () => (
  <Svg width={400} height={400} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <CoordinateSystem xDomain={[-4, 4]} yDomain={[-4, 4]}>
      <Hull
        points={[
          { x: 1, y: 2 },
          { x: 2, y: 3 },
          { x: 5, y: 10 },
        ]}
        color="transparent"
        outlineColor="red"
        outlineWidth="6"
      />
    </CoordinateSystem>
  </Svg>
);
```

#### Свойства

| Свойство      | Тип          | По умолчанию   | Описание                                    |
| ------------- | ------------ | -------------- | ------------------------------------------- |
| points        | `TPoint[]`   | —              | Набор точек, для которых строится оболочка. |
| color?        | `string`     | `currentColor` | Цвет оболочки.                              |
| outlineColor? | `string`     | `transparent`  | Цвет обводки.                               |
| outlineWidth? | `number`     | `1`            | Ширина обводки.                             |
| className?    | `string`     | —              | Дополнительный класс.                       |
| onClick?      | `() => void` | —              | Обработчик клика.                           |

## Стилизация

Для гибкой настройки к каждому компоненту можно примиксовать `className`.

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/CoordinateSystem)
