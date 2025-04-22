# org-names

```js
{
    block: 'org-names',
    js: true,
    content: [
        {
            elem: 'name',
            content: 'Явное лучше неявного'
        },
        {
            elem: 'name',
            elemMods: { hidden: true },
            content: 'Интриги'
        },
        {
            elem: 'name',
            elemMods: { hidden: true },
            content: 'скандалы'
        },
        {
            elem: 'name',
            elemMods: { hidden: true },
            content: 'расследования'
        },
        {
            block: 'link',
            mods: { theme: 'islands', pseudo: true },
            mix: { block: 'org-names', elem: 'more', js: true },
            content: 'Показать все, что скрыто'
        }
    ]
}
```
