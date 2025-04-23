## Functions

<dl>
<dt><a href="#setParams">`setParams(params)`</a></dt>
<dd><p>Устанавливает сохраненные параметры фильтра
Перерисовывает форму, если необходимо</p>
</dd>
<dt><a href="#clear">`clear()`</a></dt>
<dd><p>Очистить фильтр</p>
</dd>
</dl>

## Events

<dl>
<dt><a href="#event_change">`"change"`</a> ⇐ <code>BEM.DOM</code></dt>
<dd><p>Слой абстракции над фильтрами
Добавляет в блок логику загрузки,
отрисовки, изменения, сброса значений в форме</p>
</dd>
<dt><a href="#event_change">`"change" (data)`</a></dt>
<dd></dd>
<dt><a href="#event_Submit">`"Submit" (e, data)`</a></dt>
<dd><p>Сабмит формы фильтра</p>
</dd>
</dl>

<a name="setParams"></a>

## `setParams(params)`
Устанавливает сохраненные параметры фильтра
Перерисовывает форму, если необходимо

**Kind**: global function  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="clear"></a>

## `clear()`
Очистить фильтр

**Kind**: global function  
**Emits**: [<code>change</code>](#event_change)  
<a name="event_change"></a>

## `"change"` ⇐ <code>BEM.DOM</code>
Слой абстракции над фильтрами
Добавляет в блок логику загрузки,
отрисовки, изменения, сброса значений в форме

**Kind**: event emitted  
**Extends**: <code>BEM.DOM</code>  
**Author**: demzmound  
**Example**  
```js
{
    block: 'fa-filter',
    js: {
        params: {…}, // Значения параметров фильтра
        fields: […], // Список полей фильтра
        formUrl: {host: '', pathname: ''} // Url для отправки фильтров
    }
}
```
<a name="event_change"></a>

## `"change" (data)`
**Kind**: event emitted  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.data | <code>Object</code> | — параметры фильтра |
| data.changed | <code>Object</code> | — параметры фильтра отличающиеся от значений по умолчанию |

<a name="event_Submit"></a>

## `"Submit" (e, data)`
Сабмит формы фильтра

**Kind**: event emitted  

| Param | Type | Description |
| --- | --- | --- |
| e | <code>Event</code> |  |
| data | <code>Object</code> | параметры фильтра |

