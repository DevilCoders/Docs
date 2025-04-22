# Иконки

Каждая иконка является отдельным компонентом

## SvgIcon

Базовый компонент, на основе которого строятся иконки

```tsx
interface SvgIconProps extends SVGProps<SVGSVGElement> {
    width?: string
    height?: string
    color?: string
    viewBox?: string
}

export const SvgIcon: FC<SvgIconProps> = (
    {
        viewBox = "0 0 24 24",
        color,
        children,
        ...props
    }
) => (
    <svg
        viewBox={viewBox}
        {...props}
    >
        {props.children}
    </svg>
)
```

## CrossIcon

```tsx
export const ArrowIcon: FC<SvgIconProps> = (props) => (
    <SvgIcon {...props}>
        <path d="" fill={props.color} />
    </SvgIcon>
)
```

## ArrowIcon

```tsx
const enum ArrowIconDirection {
    Left,
    Right,
    Up,
    Down
}

interface ArrowIconProps extends SvgIconProps {
    direction: ArrowIconDirection
}

export const ArrowIcon: FC<ArrowIconProps> = ({ direction, ...props }) => (
    <SvgIcon {...props}>
        <path d="" fill={props.color} />
    </SvgIcon>
)
```
