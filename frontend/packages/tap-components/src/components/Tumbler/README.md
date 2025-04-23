# Tumbler

Компонент, предназначенный для создания переключателя.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { compose } from '@bem-react/core';
import {
    Tumbler as TumblerBase,
    withSizeM,
    withViewDefault,
} from '@yandex-int/tap-components/Tumbler';

const Tumbler = compose(withSizeM, withViewDefault)(TumblerBase);

const App: React.FC = () => {
    const [checked, setChecked] = useState('');

    return (
      <Tumbler
          view="default"
          size="m"
          checked={checked}
          onChange={() => setChecked(!checked)}
      />
    )
}
```

## Пример

{{%story:::tap-components-components-tumbler--playground%}}

## Свойства

| Свойство | Тип | Описание |
| -------- | -------------------------- | ------------------------ |
| autoFocus? | `false \| true` | Устанавливает фокус в компонент при монтировании |
| checked | `false \| true` | Состояние переключателя |
| className? | `string` | Дополнительный класс у корневого DOM-элемента |
| controlRef? | `RefObject<HTMLInputElement>` | Ссылка на нативный DOM-элемент нативного инпута |
| disabled? | `false \| true` | Неактивное состояние переключателя |
| id? | `string` | Уникальный id компонента |
| innerRef? | `RefObject<HTMLSpanElement>` | Ссылка на корневой DOM-элемент компонента |
| labelAfter? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Подпись после переключателя |
| labelBefore? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Подпись перед переключателем |
| name? | `string` | Имя переключателя в форме |
| onBlur? | `(event: FocusEvent<HTMLButtonElement>) => void` | Обработчик, который вызывается при потере фокуса переключателем |
| onChange | `(event: ChangeEvent<HTMLInputElement>) => void` | Обработчик, который вызывается при изменении состояния |
| onClick? | `(event: MouseEventHandler<HTMLElement>) => void` | Обработчик, который вызывается при нажатии на переключатель |
| onFocus? | `(event: FocusEvent<HTMLButtonElement>) => void` | Обработчик, который вызывается при получении фокуса переключателем |
| onKeyDown? | `(event: KeyboardEvent<HTMLButtonElement>) => void` | Обработчик, который вызывается при нажатии клавиши на клавиатуре (при этом переключатель должен быть в фокусе) |
| onKeyUp? | `(event: KeyboardEvent<HTMLButtonElement>) => void` | Обработчик, который вызывается при отжатии клавиши на клавиатуре (при этом переключатель должен быть в фокусе) |
| required? | `false \| true` | Устанавливает в компоненте обязательное состояние |
| tabIndex? | `number` | Целое число, определяющее, должен ли переключатель участвовать в последовательной навигации по всей странице с помощью клавиатуры |
| title? | `string` | Всплывающая подсказка |
