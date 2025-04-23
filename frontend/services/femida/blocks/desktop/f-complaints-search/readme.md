<a name="module_f-complaints-search"></a>

## f-complaints-search ⇐ <code>BEM.DOM</code>
Поиск по жалобам

**Extends**: <code>BEM.DOM</code>  
**Author**: olgakozlova  
**Example**  
```js
{
    block: 'f-complaints-search',
    js: {
        filter: {...},
        fields: [...]
    }
}
```

* [f-complaints-search](#module_f-complaints-search) ⇐ <code>BEM.DOM</code>
    * [`~clear()`](#module_f-complaints-search..clear)
    * [`~submit()`](#module_f-complaints-search..submit)
    * [`~_updateFilterCount(params)`](#module_f-complaints-search.._updateFilterCount)
    * [`~setFilter(filter)`](#module_f-complaints-search..setFilter)
    * [`"search" (data)`](#event_search)
    * [`"search" (data)`](#event_search)

<a name="module_f-complaints-search..clear"></a>

### `f-complaints-search~clear()`
Очистить фильтр

**Kind**: inner method of [<code>f-complaints-search</code>](#module_f-complaints-search)  
<a name="module_f-complaints-search..submit"></a>

### `f-complaints-search~submit()`
Применить фильтр

**Kind**: inner method of [<code>f-complaints-search</code>](#module_f-complaints-search)  
<a name="module_f-complaints-search.._updateFilterCount"></a>

### `f-complaints-search~\_updateFilterCount(params)`
Обновляет счетчик выбранных фильтров

**Kind**: inner method of [<code>f-complaints-search</code>](#module_f-complaints-search)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-complaints-search..setFilter"></a>

### `f-complaints-search~setFilter(filter)`
Устанавливает сохраненные фильтры
Перерисовывает форму, если необходимо

**Kind**: inner method of [<code>f-complaints-search</code>](#module_f-complaints-search)  

| Param | Type |
| --- | --- |
| filter | <code>Object</code> | 

<a name="event_search"></a>

### `"search" (data)`
**Kind**: event emitted by [<code>f-complaints-search</code>](#module_f-complaints-search)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> | параметры фильтра |
| data.data | <code>Object</code> | данные |
| data.reason | <code>Object</code> | причина изменений |

<a name="event_search"></a>

### `"search" (data)`
**Kind**: event emitted by [<code>f-complaints-search</code>](#module_f-complaints-search)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> | параметры фильтра |
| data.data | <code>Object</code> | данные |
| data.reason | <code>Object</code> | причина изменений |

