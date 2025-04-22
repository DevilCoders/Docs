# Текстовые компоненты ввода

Скорее всего, будет базовый компонент Input, на основе которого будут строиться другие инпуты

## TextField

```tsx
// Размер поля задается на основе его высоты
const enum TextFieldSize {
    S20 = 20,
    S40 = 40
}

const enum TextFieldType {
    Number = 'number',
    Password = 'password',
    Type = 'type',
    Tel = 'tel',
    Text = 'text',
    Url = 'url',
    Email = 'email',
    Search = 'search'
}

interface TextField {
    value: string
    type?: TextFieldType
    placeholder?: string
    withAutoFocus?: boolean
    isAutoComplete?: boolean
    maxLength?: number
    name?: string
    tabIndex?: number
    isDisabled?: boolean
    error?: React.ReactNode
    // Подсказка возле поля
    hint?: React.ReactNode
    iconLeft?: React.ReactNode
    iconRight?: React.ReactNode
    title?: string
    // Маска поля из регулярного выражения
    mask?: string
    size?: TextFieldSize
    hasClear?: boolean
    onChange?: (value: string) => void
    onClick?: React.MouseEventHandler
    onFocus?: React.MouseEventHandler
    onBlur?: React.MouseEventHandler
    onKeyPress?: React.KeyboardEventHandler
    onKeyDown?: React.KeyboardEventHandler
    onKeyUp?: React.KeyboardEventHandler
}
```

## TextareaField

```tsx
interface TextareaField {
    value: string
    placeholder?: string
    withAutoFocus?: boolean
    isAutoComplete?: boolean
    maxLength?: number
    name?: string
    tabIndex?: number
    isDisabled?: boolean
    error?: React.ReactNode
    minRows?: number
    maxRows?: number
    hint?: React.ReactNode
    iconLeft?: React.ReactNode
    iconRight?: React.ReactNode
    title?: string
    hasClear?: boolean
    onChange?: (value: string) => void
    onClick?: React.MouseEventHandler
    onFocus?: React.MouseEventHandler
    onBlur?: React.MouseEventHandler
    onKeyPress?: React.KeyboardEventHandler
    onKeyDown?: React.KeyboardEventHandler
    onKeyUp?: React.KeyboardEventHandler
}
```
