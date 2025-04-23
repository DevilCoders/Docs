<a name="module_f-vac-group-action"></a>

## f-vac-group-action ⇐ <code>fa-bb-model</code>
Действие над группой вакансий

**Extends**: <code>fa-bb-model</code>  
**Author**: ertema  
**Example**  
```js
// Действие кнопка
{
    block: 'f-vac-group-action',
    mods: {
        switcher: 'button',
        size: 'm',
        action: 'update'
    },
    id: 1 // Для update обязательно нужно передать id
}
```
**Example**  
```js
// Отключенное действие
{
    block: 'f-vac-group-action',
    mods: {
        switcher: 'button',
        size: 'm',
        action: 'activate',
        disabled: true
    }
}
```
**Example**  
```js
// Действие в меню
{
    block: 'f-vac-group-action',
    mods: {
        switcher: 'menu-item',
        action: 'deactivate'
    }
}
```
