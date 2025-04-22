<a name="module_f-search"></a>

## f-search ⇐ <code>BEM.DOM</code>
Поисковое поле

**Extends**: <code>BEM.DOM</code>  
**Author**: natamaki  
**Example**  
```js
{
    block: 'f-search',
    mods: {
        'with-settings': Boolean,
        settings: Boolean // Только с with-settings
    },
    name: String,
    placeholder: String,
    value: String
}
```

* [f-search](#module_f-search) ⇐ <code>BEM.DOM</code>
    * [`~val()`](#module_f-search..val) ⇒ <code>String</code>
    * [`"submit"`](#event_submit)
    * [`"change"`](#event_change)

<a name="module_f-search..val"></a>

### `f-search~val()` ⇒ <code>String</code>
**Kind**: inner method of [<code>f-search</code>](#module_f-search)  
**See**: input.val  
<a name="event_submit"></a>

### `"submit"`
Поиск

**Kind**: event emitted by [<code>f-search</code>](#module_f-search)  
**Params**: <code>Object</code> data  
**Params**: <code>String</code> data.text  
<a name="event_change"></a>

### `"change"`
Изменение запроса

**Kind**: event emitted by [<code>f-search</code>](#module_f-search)  
**Params**: <code>Object</code> data  
**Params**: <code>String</code> data.text  
