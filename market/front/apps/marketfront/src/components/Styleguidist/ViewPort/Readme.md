Оборачивает переданную ноду в `iframe`.

Используется в Стайлгайдисте для тестирования компонента для различных media-queries.

### Параметры

#### `width` & `height`


```jsx

const sizes = [
    {width: 100, height: 100},
    {width: 200, height: 200},
    {width: 300, height: 300},
];

<div>
    {sizes.map(size => (
        <div style={{marginTop: '20px'}}>
            <ViewPort width={size.width} height={size.height}>
                 {size.width}x{size.height}
            </ViewPort>
        </div>
    ))}
</div>
```
