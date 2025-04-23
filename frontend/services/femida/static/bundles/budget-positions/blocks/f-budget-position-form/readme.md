<a name="module_f-budget-position-form"></a>

## f-budget-position-form ⇐ <code>BEM.DOM</code>
**Extends**: <code>BEM.DOM</code>  
**Author**: annvas  
**Example**  
```js
// Форма создания
{
    block: 'f-budget-position-form',
    mods: {type: 'create'},
    data: {structure: {…}}
}
// Форма редактирования
{
    block: 'f-budget-position-form',
    mods: {type: 'edit'},
    data: {structure: {…}, data: {…}},
    id: 123
}
 * // Форма поиска
{
    block: 'f-budget-position-form',
    mods: {type: 'search'},
    data: {…},
}
```
<a name="module_f-budget-position-form..getForm"></a>

### `f-budget-position-form~getForm()` ⇒ <code>BEM.DOM</code>
Возвращает s-form блока

**Kind**: inner method of [<code>f-budget-position-form</code>](#module_f-budget-position-form)  
