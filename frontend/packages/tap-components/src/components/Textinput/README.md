# Textinput

Однострочное текстовое поле.

## Пример использования

```typescript jsx
import React, { useState } from 'react'
import { compose } from '@bem-react/core'
import {
    Textinput as TextinputBase,
    withViewMaterial,
    withSizeM,
} from '@yandex-int/tap-components/Textinput'

// Композиция из различных модификаторов
const Textinput = compose(withViewMaterial, withSizeM)(TextinputBase)

const App: React.FC = () => {
    const [value, setValue] = useState('')

    return (
      <Textinput
          size="m"
          view="material"
          value={value}
          onChange={(event) => setValue(event.target.value)}
      />
    )
}
```

## Пример

{{%story:::tap-components-components-textinput--playground%}}

## Свойства

| Свойство | Тип | Описание |
| ------------- | ---------------------------------------------------------- | --------------------------------------------- |
| addonAfter? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Дополнительный контент после контрола |
| addonBefore? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Дополнительный контент перед контролом |
| autoComplete? | `string` | HTML-атрибут `autocomplete` |
| autoFocus? | `false \| true` | HTML-атрибут `autofocus` |
| className? | `string` | Дополнительный класс у корневого DOM-элемента |
| controlRef? | `(instance: HTMLInputElement) => void \| RefObject<HTMLInputElement>` | Ссылка на DOM элемент нативного инпута |
| defaultValue? | `string \| number` | Значение по умолчанию контрола |
| disabled? | `false \| true` | HTML-атрибут `disabled` |
| focused? | `false \| true` | Состояние фокуса на компоненте |
| hasClear? | `false \| true` | Наличие крестика для очистки текстового поля |
| hint? | `string` | Текст-подсказка, появляющаяся после компонента. Может иметь различное визуальное оформление в зависимости от свойства `state` |
| iconLeft? | `ReactElement<IIconProps, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)>` | Иконка слева от содержимого текстового поля |
| iconRight? | `ReactElement<IIconProps, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)>` | Иконка справа от содержимого текстового поля |
| id? | `string` | Уникальный id компонента |
| innerRef? | `(instance: HTMLSpanElement) => void \| RefObject<HTMLSpanElement>` | Ссылка на корневой DOM элемент компонента |
| inputMode? | `"decimal" \| "numeric" \| "text" \| "url" \| "email" \| "search" \| "tel"` | HTML-атрибут `inputmode` |
| max? | `number` | Максимальное значение при использовании `type=number` |
| maxLength? | `number` | Максимальное количество символов, которое можно ввести в текстовое поле |
| min? | `number` | Минимальное значение при использовании `type=number` |
| name? | `string` | Имя компонента |
| onBlur? | `(event: FocusEvent<HTMLInputElement>) => void` | Обработчик, вызываемый при срабатывании события blur |
| onChange? | `(event: ChangeEvent<HTMLInputElement>) => void` | Обработчик изменения значения |
| onClearClick? | `(event: MouseEventHandler<HTMLElement>) => void` | Обработчик клика по крестику. |
| onClick? | `(event: MouseEventHandler<HTMLElement>) => void` | Событие, которое вызывается при нажатии на компонент |
| onFocus? | `(event: FocusEvent<HTMLInputElement>) => void` | Обработчик, вызываемый при срабатывании события focus |
| onKeyDown? | `(event: KeyboardEvent<HTMLInputElement>) => void` | Обработчик, вызываемый при срабатывании события keydown |
| onKeyPress? | `(event: KeyboardEvent<HTMLInputElement>) => void` | Обработчик, вызываемый при срабатывании события keypress |
| onKeyUp? | `(event: KeyboardEvent<HTMLInputElement>) => void` | Обработчик, вызываемый при срабатывании события keyup |
| pattern? | `string` | Шаблон, используемый для проверки значения при отправке формы |
| placeholder? | `string` | Плейсхолдер |
| pressed? | `false \| true` | Состояние нажатия на компоненте |
| readOnly? | `false \| true` | Запрещает изменять значение в текстовом поле |
| required? | `false \| true` | Устанавливает в компоненте обязательное состояние |
| state? | `"error"` | Визуальное состояние компонента. Может использоваться при проверке формы на корректность |
| style? | `CSSProperties` | Пользовательские стили на корневом DOM элементе |
| tabIndex? | `number` | Целое число, определяющее, должен ли переключатель участвовать в последовательной навигации по всей странице с помощью клавиатуры |
| title? | `string` | Всплывающая подсказка |
| type? | `string` | HTML-атрибут `type` |
| value? | `string \| number` | Значение контрола |