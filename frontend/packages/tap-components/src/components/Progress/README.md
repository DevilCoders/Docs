# Progress

Компонент для создания полосы прогресса.

## Пример использования

```typescript jsx
import React from 'react'
import { Progress } from '@yandex-int/tap-components/Progress'

const App: React.FC = () => {
    return <Progress timing="linear" value={50} maxValue={100}/>
}
```

## Пример

{{%story:::tap-components-components-progress--playground%}}

## Свойства

| Свойство   | Тип                         | По умолчанию | Описание                                                 |
| ---------- | --------------------------- | ------------ | -------------------------------------------------------- |
| className? | `string`                    | —            | Дополнительный класс у корневого DOM-элемента            |
| innerRef?  | `RefObject<HTMLDivElement>` | —            | Ссылка на корневой DOM-элемент компонента                |
| maxValue?  | `number`                    | `1`          | Максимальное допустимое значение прогресс бара           |
| style?     | `CSSProperties`             | —            | Пользовательские стили                                   |
| timing?    | `"linear"`                  | —            | Способ CSS-анимации при изменении ширины полосы загрузки |
| value?     | `number`                    | `0`          | Доля загрузки прогресс бара от 0 до maxValue             |
