<a name="module_f-problems-filter"></a>

## f-problems-filter ⇐ <code>BEM.DOM</code>
Фильтр для страницы поиска задач
Загружает форму по переданным параметрам

**Extends**: <code>BEM.DOM</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-problems-filter',
    js: {
        params: {…}, // Значения параметров фильтра
        fields: […] // Список параметров фильтра
    }
}
```

* [f-problems-filter](#module_f-problems-filter) ⇐ <code>BEM.DOM</code>
    * [`~setParams(params)`](#module_f-problems-filter..setParams)
    * [`~applyForm()`](#module_f-problems-filter..applyForm) ⇒ <code>Object</code>
    * [`~clear()`](#module_f-problems-filter..clear)
    * [`~submit()`](#module_f-problems-filter..submit)
    * [`"change" (data)`](#event_change)
    * [`"Submit" (e, data)`](#event_Submit)

<a name="module_f-problems-filter..setParams"></a>

### `f-problems-filter~setParams(params)`
Устанавливает сохраненные параметры фильтра
Перерисовывает форму, если необходимо

**Kind**: inner method of [<code>f-problems-filter</code>](#module_f-problems-filter)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-problems-filter..applyForm"></a>

### `f-problems-filter~applyForm()` ⇒ <code>Object</code>
Заменяет сохраненные параметры фильтра на выбранные в форме фильтра

**Kind**: inner method of [<code>f-problems-filter</code>](#module_f-problems-filter)  
**Returns**: <code>Object</code> - новые параметры фильра  
<a name="module_f-problems-filter..clear"></a>

### `f-problems-filter~clear()`
Очистить фильтр

**Kind**: inner method of [<code>f-problems-filter</code>](#module_f-problems-filter)  
<a name="module_f-problems-filter..submit"></a>

### `f-problems-filter~submit()`
Применить фильтр

**Kind**: inner method of [<code>f-problems-filter</code>](#module_f-problems-filter)  
<a name="event_change"></a>

### `"change" (data)`
**Kind**: event emitted by [<code>f-problems-filter</code>](#module_f-problems-filter)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.data | <code>Object</code> | — параметры фильтра |
| data.changed | <code>Object</code> | — параметры фильтра отличающиеся от значений по умолчанию |

<a name="event_Submit"></a>

### `"Submit" (e, data)`
Сабмит формы фильтра

**Kind**: event emitted by [<code>f-problems-filter</code>](#module_f-problems-filter)  

| Param | Type | Description |
| --- | --- | --- |
| e | <code>Event</code> |  |
| data | <code>Object</code> | параметры фильтра |

