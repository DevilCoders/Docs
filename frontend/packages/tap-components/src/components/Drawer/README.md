# Drawer

Компонент для создания шторки.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { compose } from '@bem-react/core';
import { Drawer as DrawerBase, withViewDefault } from '@yandex-int/tap-components/Drawer';

const Drawer = compose(withViewDefault)(DrawerBase);

const App: React.FC = () => {
  const scopeRef = React.useRef<HTMLDivElement>(null)
  const [visible, setVisible] = React.useState(false)
  const openDrawer = React.useCallback(() => setVisible(true), [])
  const closeDrawer = React.useCallback(() => setVisible(false), [])

  return (
    <div ref={scopeRef}>
      <button onClick={openDrawer}>Открыть шторку</button>
      <Drawer visible={visible} onClose={closeDrawer} scope={scopeRef} view="default">
        <p>Содержимое шторки</p>
        <button onClick={closeDrawer}>Закрыть шторку</button>
      </Drawer>
    </div>
  )
}
```

## Пример

{{%story:::tap-components-components-drawer--playground%}}

## Вложенные шторки

При открытии шторки поверх другой меняется внешний вид, это достигается установкой свойства `nested` в значение `true`.

> **Примечание.** Шторка самостоятельно не умеет отслеживать другие шторки на странице, поэтому взаимодействие нескольких шторок необходимо реализовывать дополнительно.

## Свойства

| Свойство        | Тип | По умолчанию | Описание |
| --------------- | ----------------------------------------------------------- |
| animation       | `IDrawerAnimationParams` | — | Параметры анимации шторки. |
| className?      | `string` | — | Дополнительный класс у корневого DOM-элемента |
| direction?      | `"bottom" \| "left" \| "right"` | — | Направление, откуда появляется шторка. |
| dragDisabled?   | `false \| true` | — | Делает шторку «статичной» |
| innerRef?       | `(instance: HTMLDivElement) => void \| RefObject<HTMLDivElement>` | — | Ссылка на корневой DOM-элемент компонента |
| keepMounted?    | `false \| true` | `true` | Сохраняет контейнер в DOM после создания |
| maxSize?        | `string` | — | Максимальный размер шторки (ширина или высота в зависимости от свойства `direction`). Принимает любое валидное CSS значение. |
| nested?         | `false \| true` | — | Меняет внешний вид для режима "шторка внутри шторки". |
| onClose?        | `() => void` | — | Обработчик закрытия шторки |
| scope?          | `RefObject<HTMLElement>` | `document.body` | Ссылка на DOM-элемент, в котором размещается попап<br>Важно, чтобы контейнер имел `position: relative` для корректного позициоинирования. |
| titleComponent? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — | Компонент шапки шторки |
| visible?        | `false \| true` | — | Делает попап видимым |
| zIndex?         | `number` | — | Задает слой `z-index` |
