# Svg

<!-- description:start -->
Компонент-контейнер для svg по [конвенции](https://observablehq.com/@d3/margin-convention).
<!-- description:end -->

## Пример использования

```typescript jsx
import React from 'react';
import { Svg, useSvgContext } from '@yandex-int/edu-components/Svg/desktop';

// Пример дочернего компонента
const SvgText = () => {
  const { width, height } = useSvgContext('Svg text');

  return (
    <text>
      inner width: {width}, inner height {height}
    </text>
  );
};

const App = () => (
  <Svg width={500} height={500} margin={{ top: 25, right: 25, bottom: 25, left: 25 }}>
    <SvgText />
  </Svg>
);
```

## Свойства

<!-- props:start -->
| Свойство   | Тип                                                             | Описание                       |
| ---------- | --------------------------------------------------------------- | ------------------------------ |
| width      | `number`                                                        | Ширина svg без учёта отступов. |
| height     | `number`                                                        | Высота svg без учёта отступов. |
| margin?    | `{ top: number; right: number; bottom: number; left: number; }` | Размеры отступов.              |
| className? | `string`                                                        | Дополнительный класс.          |
| innerRef?  | `(instance: SVGSVGElement) => void \| RefObject<SVGSVGElement>` | Ссылка на корневой DOM-узел.   |
<!-- props:end -->

## Модификаторы
<!-- modifiers:start -->
# scalable

Модификатор, отвечающий за возможность масштабирования компонента `Svg`.

В контекст пробрасывается текущее значение масштаба, элементы реализуют реакцию на изменение.

Масштаб изменяется на следующие действия:

-   Двойной клик - увеличение масштаба
-   Колёсико вверх - увеличение масштаба
-   Колёсико вниз - уменьшение масштаба

| Свойство       | Тип                                                      | Описание                                                                                                          |
| -------------- | -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| scalable?      | `false \| true`                                          | Флаг масштабирования.                                                                                             |
| scale?         | `number`                                                 | Значение масштаба.                                                                                                |
| onScaleChange? | `(newScale: number) => void`                             | Обработчик изменения масштаба.                                                                                    |
| scaleOptions?  | `{ wheelScaleStep: number; dblClickScaleStep: number; }` | Опции масштабирования.<br>_ wheelScaleStep - шаг для колёсика мыши _ dblClickScaleStep - шаг для двойного нажатия |
<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Svg)
