# Кнопка

```tsx
// Размер кнопки задается на основе ее высоты
const enum ButtonSize {
    S44 = 44,
    S32 = 32
}

const enum ButtonView {
    Yellow,
    White,
    Beige
}

const enum ButtonType {
    Basic,
    Action
}

const enum ButtonShape {
    Circle,
    Rectangle
}

// Auto - кнопка по размеру контента, Max - тянется по ширине контейнера
const enum ButtonWidth {
    Auto,
    Max
}

// Обычная кнопка, может иметь иконки слева/справа от текста, не может быть круглой
interface TextButtonProps {
    // Текст кнопки
    children: string;
    type: ButtonType;
    width?: ButtonWidth;
    iconLeft?: React.ReactNode;
    iconRight?: React.ReactNode;
}

// Кнопка с иконкой без текста
interface IconButtonProps {
    icon: React.ReactNode;
}

type ButtonProps = {
    size: ButtonSize;
    view: ButtonView;
    isDisabled?: boolean;
    isInProgress?: boolean;
    className?: string;
    shape?: ButtonShape;
    onClick?: React.MouseEventHandler;
    onFocus?: React.FocusEventHandler;
    onBlur?: React.FocusEventHandler;
} & (TextButtonProps | IconButtonProps);
```
