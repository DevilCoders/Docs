<a name="module_f-problems-search"></a>

## f-problems-search ⇐ <code>BEM.DOM</code>
Поиск по задачам

**Extends**: <code>BEM.DOM</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-problems-search',
    mods: {
        expanded: Boolean
    }
    filter: {…} // параметры фильтра и поисковый запрос
    fields: […] // поля фильтра
}
```

* [f-problems-search](#module_f-problems-search) ⇐ <code>BEM.DOM</code>
    * [`~setFilter(params)`](#module_f-problems-search..setFilter)
    * [`~_updateFilterCount(count)`](#module_f-problems-search.._updateFilterCount)
    * [`~destruct()`](#module_f-problems-search..destruct) ⇒ <code>\*</code>
    * [`"search" (data)`](#event_search)

<a name="module_f-problems-search..setFilter"></a>

### `f-problems-search~setFilter(params)`
Задаёт параметры фильтра

**Kind**: inner method of [<code>f-problems-search</code>](#module_f-problems-search)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-problems-search.._updateFilterCount"></a>

### `f-problems-search~\_updateFilterCount(count)`
Обновляет счетчик выбранных фильтров

**Kind**: inner method of [<code>f-problems-search</code>](#module_f-problems-search)  

| Param | Type |
| --- | --- |
| count | <code>Number</code> | 

<a name="module_f-problems-search..destruct"></a>

### `f-problems-search~destruct()` ⇒ <code>\*</code>
**Kind**: inner method of [<code>f-problems-search</code>](#module_f-problems-search)  
**See**: BEM.DOM.desctruct  
<a name="event_search"></a>

### `"search" (data)`
Поиск

**Kind**: event emitted by [<code>f-problems-search</code>](#module_f-problems-search)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.filter | <code>Object</code> |  |
| data.reason | <code>&#x27;search-submit&#x27;</code> \| <code>&#x27;filter-submit&#x27;</code> \| <code>&#x27;filter-change&#x27;</code> | причина события |

