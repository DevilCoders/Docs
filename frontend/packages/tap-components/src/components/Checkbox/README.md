# Checkbox

Компонент для создания чекбоксов различных типов.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { compose } from '@bem-react/core';
import {
    Checkbox as CheckboxBase,
    withSizeM,
    withViewDefault,
} from '@yandex-int/tap-components/Checkbox';

const Checkbox = compose(withSizeM, withViewDefault)(CheckboxBase);

const App: React.FC = () => {
    const [checked, setChecked] = useState(false)

    return (
        <Checkbox
            label="checkbox"
            size="m"
            view="default"
            onChange={() => setChecked(!checked)}
            checked={checked}
        />
    );
};
```

## Пример

{{%story:::tap-components-components-checkbox--playground%}}

## Свойства

| Свойство | Тип | Описание |
| -------- | --- | -------- |
| autoFocus? | `false \| true` | Устанавливает фокус в компонент при монтировании |
| checked? | `false \| true` | Состояние переключателя: включен или выключен |
| className? | `string` | Дополнительный класс у корневого DOM-элемента |
| controlRef? | `(instance: T) => void \| RefObject<T>` | Ссылка на DOM-элемент нативного контрола |
| disabled? | `false \| true` | Неактивное состояние компонента. Состояние, при котором компонент отображается, но недоступен для действий пользователя |
| focused? | `false \| true` | Состояние фокуса на компоненте |
| id? | `string` | Уникальный id компонента |
| indeterminate? | `false \| true` | Визуально переводит чекбокс в неопределенное состояние. Не влияет на состояние, указанное в `checked`.<br>Может использоваться в дереве чекбоксов, чтобы показать состояние родительского чекбокса, когда хотя бы один вложенный чекбокс отмечен, но не все.<br>Если свойство задано родительскому чекбоксу, то в `aria-controls` необходимо добавить `id` всех вложенных чекбоксов |
| innerRef? | `(instance: HTMLElement) => void \| RefObject<HTMLElement>` | Ссылка на корневой DOM-элемент компонента |
| label? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Текст подписи к чекбоксу |
| name? | `string` | Имя компонента |
| onChange? | `(event: ChangeEvent<HTMLInputElement>) => void` | Обработчик изменения значения |
| onClick? | `(event: MouseEvent<HTMLElement>) => void` | Событие, которое вызывается при нажатии на компонент |
| onBlur?  | `(event: FocusEvent<HTMLElement>) => void` | Событие, которое вызывается при потере фокуса компонентом. Например, при клике на другом месте экрана |
| onFocus? | `(event: FocusEvent<HTMLElement>) => void` | Событие, которое возникает при получении компонентом фокуса |
| pressed? | `false \| true` | Состояние нажатия на компоненте |
| required? | `false \| true` | Устанавливает в компоненте обязательное состояние |
| tabIndex? | `number` | Целое число, определяющее должен ли переключатель участвовать в последовательной навигации по всей странице с помощью клавиатуры |
| title? | `string` | Всплывающая подсказка |
