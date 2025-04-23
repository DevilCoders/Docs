Переключатель состояния для collapsable компонентов.

Принимает состояние collapsed (открыто/закрыто) и обработчик события onClick.

Закрытый:

```(jsx)
    <CollapseToggler
        collapsed={true}
        onClick={() => console.log("CollapseToggler (closed) was clicked")}
    />
```

Открытый:

```(jsx)
    <CollapseToggler
        collapsed={false}
        onClick={() => console.log("CollapseToggler (opened) was clicked")}
    />
```

Можно создавать кнопки разного размера, задавая модификатор

```(jsx)
    <CollapseToggler
        collapsed={true}
        size="s"
        onClick={() => console.log("CollapseToggler (opened) was clicked")}
    />
```
