# Слоты

В базовой реализации компонента "TextInput" в `props`-ах есть специальные слоты, через которые внутрь компонента можно добавлять контент.

Например, через слот `addonBefore`  реализован модификатор "hasClear":

``` tsx
<Textinput
    {...this.props}
    addonBefore={
        <>
            <Clear
                onClick={this.onClick}
                onMouseDown={this.onMouseDown}
                visible={Boolean(value)}
            />
            {addonBefore}
        </>
    }
/>
```
