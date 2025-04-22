# Ссылка

```tsx
const enum LinkSize {
    S12 = 12,
    S16 = 16,
    S18 = 18
}

const enum LinkView {
    Red,
    Grey
}

const enum LinkTarget {
    Blank = '_blank',
    Self = '_self',
    Parent = '_parent',
    Top = '_top'
}

interface LinkProps {
    // У ссылки может не быть размера, если какой-то сложный компонент оборачивается в нее
    size?: LinkSize
    // У ссылки может не быть свойства view, если какой-то сложный компонент оборачивается в нее
    view?: LinkView
    href?: string
    isDownload?: boolean
    title?: string
    target?: LinkTarget
    rel?: string
    tabIndex?: number
    role?: string
    isDisabled?: boolean
    onClick?: React.MouseEventHandler
    onFocus?: React.MouseEventHandler
    onBlur?: React.MouseEventHandler
}
```
