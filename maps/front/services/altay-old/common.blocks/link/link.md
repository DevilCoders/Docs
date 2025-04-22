# link

Доопределяет `link` из `bem-components`:

* переопределяет внешний вид ссылок `_theme_islands`
* предоставляет модификатор `_view_black`
* `_safe` (оборачивает url в hidereferer)

```js
[
    {
        block: 'link',
        mods: { theme: 'islands' },
        content: 'Обычная ссылка'
    },
    {
        block: 'link',
        mods: { theme: 'islands', view: 'black' },
        content: '_view_black'
    },
    {
        block: 'link',
        mods: { theme: 'islands', safe: true },
        url: 'http://lurkmore.to',
        content: 'Реферер будет надежно скрыт'
    }
].map(function(l) {
    return { content: l };
})
```
