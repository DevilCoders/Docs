<a name="module_f-vacancies-filter"></a>

## f-vacancies-filter ⇐ <code>BEM.DOM</code>
Фильтр для списка вакансий
Загружает форму по переданным параметрам

**Extends**: <code>BEM.DOM</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-vacancies-filter',
    js: {
        params: {…}, // Значения параметров фильтра
        fields: […] // Список параметров фильтра
    }
}
```

* [f-vacancies-filter](#module_f-vacancies-filter) ⇐ <code>BEM.DOM</code>
    * [`~setParams(params)`](#module_f-vacancies-filter..setParams)
    * [`~clear()`](#module_f-vacancies-filter..clear)
    * [`~submit()`](#module_f-vacancies-filter..submit)
    * [`~_updateFilterCount(count)`](#module_f-vacancies-filter.._updateFilterCount)
    * [`"change" (data)`](#event_change)
    * [`"Submit" (e, data)`](#event_Submit)

<a name="module_f-vacancies-filter..setParams"></a>

### `f-vacancies-filter~setParams(params)`
Устанавливает сохраненные параметры фильтра
Перерисовывает форму, если необходимо

**Kind**: inner method of [<code>f-vacancies-filter</code>](#module_f-vacancies-filter)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-vacancies-filter..clear"></a>

### `f-vacancies-filter~clear()`
Очистить фильтр

**Kind**: inner method of [<code>f-vacancies-filter</code>](#module_f-vacancies-filter)  
<a name="module_f-vacancies-filter..submit"></a>

### `f-vacancies-filter~submit()`
Применить фильтр

**Kind**: inner method of [<code>f-vacancies-filter</code>](#module_f-vacancies-filter)  
<a name="module_f-vacancies-filter.._updateFilterCount"></a>

### `f-vacancies-filter~\_updateFilterCount(count)`
Обновляет счетчик выбранных фильтров

**Kind**: inner method of [<code>f-vacancies-filter</code>](#module_f-vacancies-filter)  

| Param | Type |
| --- | --- |
| count | <code>Number</code> | 

<a name="event_change"></a>

### `"change" (data)`
**Kind**: event emitted by [<code>f-vacancies-filter</code>](#module_f-vacancies-filter)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.data | <code>Object</code> | — параметры фильтра |
| data.changed | <code>Object</code> | — параметры фильтра отличающиеся от значений по умолчанию |

<a name="event_Submit"></a>

### `"Submit" (e, data)`
Сабмит формы фильтра

**Kind**: event emitted by [<code>f-vacancies-filter</code>](#module_f-vacancies-filter)  

| Param | Type | Description |
| --- | --- | --- |
| e | <code>Event</code> |  |
| data | <code>Object</code> | параметры фильтра |

