<a name="module_f-problem"></a>

## f-problem ⇐ <code>BEM.DOM</code>
**Extends**: <code>BEM.DOM</code>  
**Author**: annvas
{
    block: 'f-problem',
    mods: {
        theme: 'narrow',
        link: true
    },
    js: {
        model: {Problem},
        headerSize: 'm',
        interview_id: 1,
        preset_id: 1,
        assignee: 'preset' | 'interview',
        add_to_preset: true,
        actions: [...],
        customActions: {...} // Bemjson
    }
 }  

* [f-problem](#module_f-problem) ⇐ <code>BEM.DOM</code>
    * [`~_onDeprecatedChange`](#module_f-problem.._onDeprecatedChange)
    * [`~isDeleted()`](#module_f-problem..isDeleted) ⇒ <code>Boolean</code>

<a name="module_f-problem.._onDeprecatedChange"></a>

### `f-problem~\_onDeprecatedChange`
Обработка изменения свойства модели is_deprecated

**Kind**: inner property of [<code>f-problem</code>](#module_f-problem)  
<a name="module_f-problem..isDeleted"></a>

### `f-problem~isDeleted()` ⇒ <code>Boolean</code>
Удалена ли задача

**Kind**: inner method of [<code>f-problem</code>](#module_f-problem)  
