# Popup
Базовый комопнент для отображения любого всплывающего компонента

## Компоненты на базе popup:

1) Notification
![image](./assets/notification.png)

2) Tooltip
![image](./assets/tooltip.png)

3) Modal
примера в библиотеке нет

4) Dropdown
![image](./assets/dropdown.png)

## Позиционирование

1. Якорь: прибить к элементу в любом направлении
1. Фиксированное положение (относительно окна/относительно какого-либо родительского контейнера) 
1. Фиксированное положение - (центр/координаты относительно левого угла)

## Компонент

```tsx
type BasePopupProps = {
    hasTail: boolean;
    closeOnOutsideClick: boolean;
    children: JSX.Element;
}
```

## Фиксированное положение

```tsx
type FixedCoordinate = {
    type: 'absolute' | 'percentage' | 'centered';
    value?: number;
}

type FixedPopupProps = {
    positionType: 'fixed';
    target: HTMLElement;
    position: {
        x: FixedCoordinate;
        y: FixedCoordinate;
    }
};
```

## Якорь
```tsx
type Coordinate = {
    type: 'absolute' | 'percentage';
    value: number;
}

type AnchorPopupProps = {
    positionType: 'anchor';
    target: HTMLElement;
    anchorPosition: {
        // вдоль какого края якоря хотим выравнивать
        mainAxis: 'top' | 'right' | 'bottom' | 'left';
        /*
            положение на оси
            для mainAxis=top:
            start - left, stop - right

            для mainAxis=right:
            start - top(right-top), stop - bottom (right-bottom)

            *хорошо подумать над названиями
        */ 
        axisPosition: 'start' | 'middle' | 'stop';
        // фиксированный сдвиг по направлению mainAxis от axisPosition
        axisPositionOffset: number;
    } 
};
```

```tsx

type PopupProps = AnchorPopupProps | FixedPopupProps;

const Popup = ({ children, target }) => {
    return ReactDOM.createPortal(children, target || document.body);
}
```
