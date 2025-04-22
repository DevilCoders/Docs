# Textarea

Многострочное текстовое поле.

## Пример использования

Использование с нужным набором модификаторов:

```typescript jsx
import React, { useState } from 'react';
import { compose } from '@bem-react/core';
import {
  Textarea as TextareaDesktop,
  withViewDefault,
  withSizeM,
} from '@yandex-int/tap-components/Textarea';

// Композиция из различных модификаторов
const Textarea = compose(withViewDefault, withSizeM)(TextareaDesktop)

const App: React.FC = () => {
  const [value, setValue] = useState('');

  return (
    <Textarea
      size="m"
      view="default"
      value={value}
      onChange={(event) => setValue(event.target.value)}
    />
  )
}
```

## Примеры

{{%story:::tap-components-components-textarea--playground%}}

## Свойства

| Свойство | Тип | Описание |
| ------------- | ---------------------------------------------------------- | --------------------------------------------- |
| addonAfter? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Дополнительный контент после контрола. |
| addonBefore? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Дополнительный контент перед контролом. |
| autoFocus? | `false \| true` | HTML-атрибут `autofocus` |
| className? | `string` | Дополнительный класс |
| cols? | `number` | HTML-атрибут `cols` |
| controlRef? | `(instance: T) => void \| RefObject<T>` | Ссылка на дом-ноду нативного контрола. |
| defaultValue? | `string` | Значение по умолчанию контрола |
| disabled? | `false \| true` | Неактивное состояние компонента. Состояние, при котором компонент отображается, но недоступен для действий пользователя |
| focused? | `false \| true` | Состояние фокуса на компоненте |
| hint? | `string` | Текст-подсказка, появляющаяся после компонента. Может иметь различное визуальное оформление в зависимости от свойства `state`. |
| id? | `string` | Уникальный id компонента |
| innerRef? | `(instance: HTMLSpanElement) => void \| RefObject<HTMLSpanElement>` | Ссылка на корневой DOM элемент компонента. |
| maxLength? | `number` | Максимальное количество символов которое можно ввести в текстовое поле |
| name? | `string` | HTML-атрибут `name` |
| onBlur? | `(event: FocusEvent<T>) => void` | Обработчик, вызываемый при срабатывании события blur |
| onChange? | `(event: ChangeEvent<HTMLTextAreaElement>) => void` | Обработчик изменения значения |
| onClick? | `(event: MouseEvent<HTMLElement, MouseEvent>) => void` | Событие, которое вызывается при нажатии на компонент |
| onFocus? | `(event: FocusEvent<T>) => void` | Обработчик, вызываемый при срабатывании события focus |
| onKeyDown? | `(event: KeyboardEvent<HTMLTextAreaElement>) => void` | Обработчик, вызываемый при срабатывании события keydown |
| onKeyPress? | `(event: KeyboardEvent<HTMLTextAreaElement>) => void` | Обработчик, вызываемый при срабатывании события keypress |
| onKeyUp? | `(event: KeyboardEvent<HTMLTextAreaElement>) => void` | Обработчик, вызываемый при срабатывании события keyup |
| placeholder? | `string` | Плейсхолдер |
| pressed? | `false \| true` | Состояние нажатия на компоненте |
| readOnly? | `false \| true` | Запрещает изменять значение в текстовом поле |
| required? | `false \| true` | Устанавливает в компоненте обязательное состояние |
| rows? | `number` | HTML-атрибут `rows` |
| state? | `"error"` | Визуальное состояние компонента. Может использоваться при проверке формы на корректность. |
| tabIndex? | `number` | Целое число, определяющее должен ли переключатель участвовать в последовательной навигации по всей странице с помощью клавиатуры |
| title? | `string` | Всплывающая подсказка |
| value? | `string` | Значение контрола |
| wrapRef? | `(instance: HTMLSpanElement) => void \| RefObject<HTMLSpanElement>` | Ссылка на враппер DOM-элемента нативного инпута. |
