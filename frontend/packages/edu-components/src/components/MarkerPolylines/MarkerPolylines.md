# MarkerPolylines

<!-- description:start -->
Компонент механики маркера соединения ломанной линии.
<!-- description:end -->

## Примеры

### Пример использования

```tsx
import React from 'react';
import { MarkerPolylines } from '@yandex-int/edu-components/MarkerPolylines/universal';

// создаем hitAreas и backgroundSrc

export const App = () => (
  <MarkerPolylines
    backgroundSrc={backgroundSrc}
    hitAreas={hitAreas}
    value={{
      '1': [
        [{ id: 'i1' }, { id: 'i2' }],
        [{ id: 'i2' }, { id: 'i3' }],
      ],
      '2': [[{ id: 'i4' }, { id: 'i5' }]],
    }}
    statuses={{
      '1': 'correct',
      '2': 'incorrect',
    }}
  />
);
```

#### Примечание

В некоторых случаях, может понадобится нормализовать координаты зон. Это необходимо, если позиция по вертикали задается не от высоты фона, а от ширины.
Для этого, перед прокидываем `hitAreas` пересчитываем координаты, в соответствии с `aspectRatio` изображения:
```ts
const aspectRatio = imageWidth / imageHeight;

const fixedHitAreas = hitAreas.map(hitArea => ({
  ...hitArea,
  height: hitArea.height * aspectRatio,
  y: hitArea.y * aspectRatio,
}));
```

## Свойства

<!-- props:start -->
| Свойство       | Тип                                                                                                                                                                                                                                                               | Описание                                                                        |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| className?     | `string`                                                                                                                                                                                                                                                          | Дополнительный класс.                                                           |
| backgroundSrc? | `string`                                                                                                                                                                                                                                                          | Ссылка на изображение, поверх которого, будут строиться линии.                  |
| backgroundAlt? | `string`                                                                                                                                                                                                                                                          | Текстовое описание фонового изображения.                                        |
| hitAreas?      | `THitArea[]`                                                                                                                                                                                                                                                      | Описание зон для соединения.                                                    |
| value          | `{ [x: string]: TConnectionIds[]; }`                                                                                                                                                                                                                              | Текущие построенный линии.                                                      |
| statuses?      | `{ [x: string]: TConnectionStatus; }`                                                                                                                                                                                                                             | Статусы построенных линий.                                                      |
| hitAreaParams? | `{ pinVisible?: boolean; final?: boolean; gravity?: THitAreaGravity; }`                                                                                                                                                                                           | Общие параметры для всех зон.                                                   |
| disabled?      | `false \| true`                                                                                                                                                                                                                                                   | Отключает интерактивность компонента.                                           |
| spinner?       | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Спинер для показа во время загрузки изображения.                                |
| onChange?      | `(e: { target: { value: Record<string, TConnectionIds[]>; }; }) => void`                                                                                                                                                                                          | Обработчик изменения ответа. Возвращает список всех линий, состоящий из id зон. |
| onLoad?        | `(event: SyntheticEvent<HTMLImageElement, Event>) => void`                                                                                                                                                                                                        | Коллбэк на загрузку изображения.                                                |
| onError?       | `(event: SyntheticEvent<HTMLImageElement, Event>) => void`                                                                                                                                                                                                        | Коллбэк на ошибку загрузки изображения.                                         |
| innerRef?      | `(instance: HTMLDivElement) => void \| RefObject<HTMLDivElement>`                                                                                                                                                                                                 | Ссылка на корневой DOM-элемент компонента.                                      |
<!-- props:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/MarkerPolylines)
- [формат](https://github.yandex-team.ru/pelican/docs/blob/master/src/formats/markers/polylines.md)
