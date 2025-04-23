<a name="module_f-presets-search"></a>

## f-presets-search ⇐ <code>BEM.DOM</code>
Поиск по пресетам

**Extends**: <code>BEM.DOM</code>  
**Author**: olgakozlova  
**Example**  
```js
{
    block: 'f-presets-search',
    mods: {
        expanded: Boolean
    }
    filter: {…} // параметры фильтра и поисковый запрос
    fields: […] // поля фильтра
}
```

* [f-presets-search](#module_f-presets-search) ⇐ <code>BEM.DOM</code>
    * [`~clear()`](#module_f-presets-search..clear)
    * [`~submit()`](#module_f-presets-search..submit)
    * [`~_updateFilterCount(params)`](#module_f-presets-search.._updateFilterCount)
    * [`"search" (data)`](#event_search)
    * [`"search" (data)`](#event_search)

<a name="module_f-presets-search..clear"></a>

### `f-presets-search~clear()`
Очистить фильтр

**Kind**: inner method of [<code>f-presets-search</code>](#module_f-presets-search)  
<a name="module_f-presets-search..submit"></a>

### `f-presets-search~submit()`
Применить фильтр

**Kind**: inner method of [<code>f-presets-search</code>](#module_f-presets-search)  
<a name="module_f-presets-search.._updateFilterCount"></a>

### `f-presets-search~\_updateFilterCount(params)`
Обновляет счетчик выбранных фильтров

**Kind**: inner method of [<code>f-presets-search</code>](#module_f-presets-search)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="event_search"></a>

### `"search" (data)`
**Kind**: event emitted by [<code>f-presets-search</code>](#module_f-presets-search)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> | параметры фильтра |
| data.data | <code>Object</code> | данные |
| data.reason | <code>Object</code> | причина изменений |

<a name="event_search"></a>

### `"search" (data)`
**Kind**: event emitted by [<code>f-presets-search</code>](#module_f-presets-search)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> | параметры фильтра |
| data.data | <code>Object</code> | данные |
| data.reason | <code>Object</code> | причина изменений |

