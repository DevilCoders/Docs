<a name="module_f-dup-case-action"></a>

## f-dup-case-action ⇐ <code>fa-bb-model</code>
Действие над дублем

**Extends**: <code>fa-bb-model</code>  
**Author**: ertema  
**Example**  
```js
// Действие кнопка
{
    block: 'f-dup-case-action',
    mods: {
        switcher: 'button',
        size: 'm',
        action: 'cancel'
    }
}
```
**Example**  
```js
// Отключенное действие
{
    block: 'f-dup-case-action',
    mods: {
        switcher: 'button',
        size: 'm',
        action: 'mark-unclear',
        disabled: true
    }
}
```
**Example**  
```js
// Действие в меню
{
    block: 'f-dup-case-action',
    mods: {
        switcher: 'menu-item',
        action: 'cancel'
    }
}
```
