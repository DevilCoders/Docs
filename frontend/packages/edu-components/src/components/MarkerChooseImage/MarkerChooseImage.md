# MarkerChooseImage

<!-- description:start -->
Компонент для отображения задач на выбор областей на изображении.
Задается условие задачи, основная картинка и список зон на этой картинке - нужно выбрать верные зоны.
<!-- description:end -->

## Пример использования

```ts
import React from 'react';
import { compose, composeU } from '@bem-react/core';
import { withRegistry, Registry } from '@bem-react/di';
import { MarkerChooseImage, cnMarkerChooseImage } from '@yandex-int/edu-components/MarkerChooseImage/desktop';
import {
  HitArea as HitAreaBase,
  withFlavorBanana as withHitAreaFlavorBanana,
  withFlavorBlueberry as withHitAreaFlavorBlueberry,
  withBadge as withHitAreaBadge,
  BadgeAlignment,
  cnHitArea
} from 'edu-components/HitArea/desktop';
import { StatusBadge as StatusBadgeBase, hasImage } from '@yandex-int/edu-components/StatusBadge/desktop';

// Собираем компонент значка статуса
const StatusBadge = compose(hasImage)(StatusBadgeBase);

// Создаем реестр для зоны выбора
const hitAreaRegistry = new Registry({ id: cnHitArea() });

// Устанавливаем элемент в реестр зоны выбора
hitAreaRegistry.statusBadge('StatusBadge', StatusBadge);

// Собираем компонент зоны выбора
const HitArea = compose(
  withRegistry(hitAreaRegistry),
  composeU(withFlavorBanana, withFlavorBlueberry),
  withBadge,
)(HitAreaBase);

// Создаем реестр
const markerChooseImageRegistry = new Registry({ id: cnMarkerChooseImage() });

// Устанавливаем в него собранный компонент
markerChooseImageRegistry.set('HitArea', HitArea);

const App = () => (
  <MarkerChooseImage
    badgeAlignment={BadgeAlignment.BottomRight}
    flavor="blueberry"
    backgroundSrc="https://plcn-test.s3.mdst.yandex.net/resources/zadacha-106286_1506681590.png"
    hitAreas={[
      {
        y: 0.024285714285714285,
        x: 0.16642857142857143,
        width: 0.09000000000000002,
        id: 'i3',
        height: 0.1542857142857143,
      },
      {
        y: 0.02,
        x: 0.305,
        width: 0.09142857142857141,
        id: 'i4',
        height: 0.15714285714285714,
      },
      {
        y: 0.018571428571428572,
        x: 0.4392857142857143,
        width: 0.0971428571428572,
        id: 'i5',
        height: 0.15714285714285714,
      },
      {
        y: 0.018571428571428572,
        x: 0.5892857142857143,
        width: 0.0842857142857143,
        id: 'i6',
        height: 0.16142857142857142,
      },
      {
        y: 0.018571428571428572,
        x: 0.7264285714285714,
        width: 0.08714285714285719,
        id: 'i7',
        height: 0.16142857142857142,
      },
    ]}
    value={[]}
    hasBadge
  />
);
```

## Свойства

<!-- props:start -->
| Свойство        | Тип                                                                                                                                                                                                                                                               | По умолчанию | Описание                                                                                                                |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------- |
| badgeAlignment? | `"top-right" \| "bottom-right" \| "center" \| "top-left" \| "bottom-left"`                                                                                                                                                                                        | —            | Расположение значка.<br>Принимает значения: _ top-right _ bottom-right _ center _ top-left \* bottom-left               |
| hitAreas?       | `THitAreaOptions[]`                                                                                                                                                                                                                                               | `[]`         | Массив координат и id зон.                                                                                              |
| backgroundSrc   | `string`                                                                                                                                                                                                                                                          | —            | Ссылка на изображение, на котором будут выбираться ответы.                                                              |
| backgroundAlt?  | `string`                                                                                                                                                                                                                                                          | —            | Текстовое описание фонового изображения.                                                                                |
| onLoad?         | `(event: SyntheticEvent<HTMLImageElement, Event>) => void`                                                                                                                                                                                                        | —            | Коллбек на загрузку изображения.                                                                                        |
| spinner?        | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —            | Спинер для показа во время загрузки.                                                                                    |
| onChange?       | `(e: { target: { value: string[]; }; }) => void`                                                                                                                                                                                                                  | —            | Обработчик выбора зоны. Возвращает значения id всех выбранных зон.                                                      |
| disabled?       | `false \| true`                                                                                                                                                                                                                                                   | `false`      | Неактивное состояние. Состояние, при котором компонент выглядит и ведет себя неактивно.                                 |
| readOnly?       | `false \| true`                                                                                                                                                                                                                                                   | `false`      | Состояние только для чтения. Состояние, при котором компонент выглядит как обычно, но изменить его значение невозможно. |
| value           | `string[]`                                                                                                                                                                                                                                                        | —            | Массив id текущих выбранных зон. По ним определяется была зона выбрана или нет.                                         |
| statuses?       | `TAnswerStatus[]`                                                                                                                                                                                                                                                 | `[]`         | Массив статусов зон. Если у зоны нет статуса, то передается `initial`.                                                  |
| innerRef?       | `RefObject<HTMLDivElement>`                                                                                                                                                                                                                                       | —            | Ссылка на корневой DOM-элемент компонента.                                                                              |
| testName?       | `string`                                                                                                                                                                                                                                                          | —            | Имя теста. Используется для построения имён элементов, которые будут помещены в data-test-name.                         |
| flavor?         | `string`                                                                                                                                                                                                                                                          | —            | Внешний вид зон выбора ответа.                                                                                          |
| hasBadge?       | `false \| true`                                                                                                                                                                                                                                                   | —            | Ставит значок статуса для зон выбора ответа.                                                                            |
| className?      | `string`                                                                                                                                                                                                                                                          | —            | Описание отсутствует.                                                                                                   |
<!-- props:end -->

## Тестирование

Если передать свойство `testName`, на маркер, изображение и зоны будут выставлены атрибуты `data-test-name`.
Рекомендуется передавать это свойство только при `NODE_ENV=testing`:

```ts
import { testNames, convertToSelectors, MarkerChooseImage } from '@yandex-int/edu-components/MarkerChooseImage/desktop';

const testName = 'myTest';

// Передайте testName в тестируемый компонент
<MarkerChooseImage
    ...
    testName={testName}
/>

// Получите селекторы для доступа к элементам
const selectors = convertToSelectors(testNames(testName));

// Используйте их в тестах
const markerSelector = selectors.marker;
const backgroundSelector = selectors.background;
const hitareaSelector = selectors.hitarea;
const checkedHitareaSelector = selectors.checkedHitarea;
```

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerChooseImage)
