# Поле option

## Option

Базовый интерфейс для Checkbox и Radio

```tsx
interface Option<T> {
    value: T
    isChecked: boolean
    withAutoFocus?: boolean
    name?: string
    tabIndex?: number
    isDisabled?: boolean
    onClick?: React.MouseEventHandler
    onFocus?: React.MouseEventHandler
    onBlur?: React.MouseEventHandler
}
```

## OptionGroup

Базовый интерфейс для CheckboxGroup и RadioGroup

```tsx
interface OptionModel<T> {
    label: React.ReactNode
    value: T
    isDisabled?: boolean
}

interface OptionGroup<T> {
    // Значения для полей
    options: OptionModel<T>
    withAutoFocus?: boolean
    name?: string
    tabIndex?: number
    isDisabled?: boolean
    onClick?: React.MouseEventHandler
    onFocus?: React.MouseEventHandler
    onBlur?: React.MouseEventHandler
}
```
