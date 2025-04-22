<a name="module_f-submissions-filter"></a>

## f-submissions-filter ⇐ <code>BEM.DOM</code>
Фильтр для страницы списка откликов
Загружает форму по переданным параметрам

**Extends**: <code>BEM.DOM</code>  
**Author**: dezmound  
**Example**  
```js
{
    block: 'f-submissions-filter',
    js: {
        params: {…}, // Значения параметров фильтра
        fields: […] // Список параметров фильтра
    }
}
```

* [f-submissions-filter](#module_f-submissions-filter) ⇐ <code>BEM.DOM</code>
    * [`~_renderForm()`](#module_f-submissions-filter.._renderForm)
    * [`~_renderClear(count)`](#module_f-submissions-filter.._renderClear)

<a name="module_f-submissions-filter.._renderForm"></a>

### `f-submissions-filter~\_renderForm()`
**Kind**: inner method of [<code>f-submissions-filter</code>](#module_f-submissions-filter)  
**See**: fa-filter._renderForm  
<a name="module_f-submissions-filter.._renderClear"></a>

### `f-submissions-filter~\_renderClear(count)`
Рендерит элемент clear

**Kind**: inner method of [<code>f-submissions-filter</code>](#module_f-submissions-filter)  

| Param | Type | Description |
| --- | --- | --- |
| count | <code>Number</code> | количество установленных фильтров |

