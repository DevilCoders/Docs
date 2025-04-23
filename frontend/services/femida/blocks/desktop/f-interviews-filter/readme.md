<a name="module_f-interviews-filter"></a>

## f-interviews-filter ⇐ <code>fa-filter</code>
Фильтр для списка секций
Загружает форму по переданным параметрам

**Extends**: <code>fa-filter</code>  
**Author**: olgakozlova  
**Example**  
```js
{
    block: 'f-interviews-filter',
    js: {
        params: {…}, // Значения параметров фильтра
        fields: […] // Список параметров фильтра
    }
}
```

* [f-interviews-filter](#module_f-interviews-filter) ⇐ <code>fa-filter</code>
    * [`~_renderForm()`](#module_f-interviews-filter.._renderForm)
    * [`~_updateFilterCount(count)`](#module_f-interviews-filter.._updateFilterCount)
    * [`~clear()`](#module_f-interviews-filter..clear)

<a name="module_f-interviews-filter.._renderForm"></a>

### `f-interviews-filter~\_renderForm()`
**Kind**: inner method of [<code>f-interviews-filter</code>](#module_f-interviews-filter)  
**See**: fa-filter._renderForm  
<a name="module_f-interviews-filter.._updateFilterCount"></a>

### `f-interviews-filter~\_updateFilterCount(count)`
Обновляет счетчик выбранных фильтров

**Kind**: inner method of [<code>f-interviews-filter</code>](#module_f-interviews-filter)  

| Param | Type |
| --- | --- |
| count | <code>Number</code> | 

<a name="module_f-interviews-filter..clear"></a>

### `f-interviews-filter~clear()`
Очистить фильтр

**Kind**: inner method of [<code>f-interviews-filter</code>](#module_f-interviews-filter)  
**Emits**: <code>event:change</code>  
