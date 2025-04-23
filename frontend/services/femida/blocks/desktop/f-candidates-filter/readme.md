<a name="module_f-candidates-filter"></a>

## f-candidates-filter ⇐ <code>fa-filter</code>
Фильтр для страницы поиска кандидатов
Загружает форму по переданным параметрам

**Extends**: <code>fa-filter</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-candidates-filter',
    js: {
        formQuery: {host: …, query: …}, // Откуда загружать форму фильтров
        params: {…} // Значения параметров фильтра
        fields: […] // Список полей фильтра
    }
}
```

* [f-candidates-filter](#module_f-candidates-filter) ⇐ <code>fa-filter</code>
    * [`~applyForm()`](#module_f-candidates-filter..applyForm) ⇒ <code>Object</code>
    * [`~submit()`](#module_f-candidates-filter..submit)
    * [`"blur" (data)`](#event_blur)
    * [`"Change" (e, data)`](#event_Change)

<a name="module_f-candidates-filter..applyForm"></a>

### `f-candidates-filter~applyForm()` ⇒ <code>Object</code>
Заменяет сохраненные параметры фильтра на выбранные в форме фильтра

**Kind**: inner method of [<code>f-candidates-filter</code>](#module_f-candidates-filter)  
**Returns**: <code>Object</code> - новые параметры фильра  
<a name="module_f-candidates-filter..submit"></a>

### `f-candidates-filter~submit()`
Применить фильтр

**Kind**: inner method of [<code>f-candidates-filter</code>](#module_f-candidates-filter)  
<a name="event_blur"></a>

### `"blur" (data)`
**Kind**: event emitted by [<code>f-candidates-filter</code>](#module_f-candidates-filter)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.data | <code>Object</code> | — параметры фильтра |
| data.changed | <code>Object</code> | — параметры фильтра отличающиеся от значений по умолчанию |

<a name="event_Change"></a>

### `"Change" (e, data)`
Сабмит формы фильтра
При котором значения в фильтре изменились

**Kind**: event emitted by [<code>f-candidates-filter</code>](#module_f-candidates-filter)  

| Param | Type | Description |
| --- | --- | --- |
| e | <code>Event</code> |  |
| data | <code>Object</code> | параметры фильтра |

