r104152
Блок attach с ограничением длины имени прикрепляемого файла

```javascript
{
    block: 'attach',
    mods: { size: 'xs', cut: 'yes' },
    limit: 18,
    content: [
        {
            block: 'button',
            mods: { size: 'xs' },
            content: iget('Выбрать файл')
        },
        {
            elem: 'holder',
            elemMods: { state: 'hidden' },
            content: iget('файл не выбран')
        }
    ]
}
```
