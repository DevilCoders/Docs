<a name="module_f-problem-action"></a>

## f-problem-action ⇐ <code>fa-bb-model</code>
Действие над задачей

**Extends**: <code>fa-bb-model</code>  
**Author**: ertema  
**Example**  
```js
// Действие
{
    block: 'f-problem-action',
    js: {
        model: {Problem}
    }
    mods: {
        size: 'm',
        action: 'edit'
    }
}
```
**Example**  
```js
// Отключенное действие
{
    block: 'f-problem-action',
    js: {
        model: {Problem}
    }
    mods: {
        size: 'm',
        action: 'print',
        disabled: true
    }
}
```
