<a name="module_f-message-form"></a>

## f-message-form ⇐ <code>BEM.DOM</code>
Форма сообщения в коммуникации по кандидату

**Extends**: <code>BEM.DOM</code>  
**Author**: annvas  
**Example**  
```js
{
    block: 'f-message-form',
    mods: {
        action: 'create', // задаёт экшн формы (здесь - создание нового сообщения)
        type: 'internal', // влияет на стили и состав полей
        for: 'candidates' // влияет на то, какая ручка будет дёргаться для загрузки и сабмита
}
```

* [f-message-form](#module_f-message-form) ⇐ <code>BEM.DOM</code>
    * [`~getApplicationChoices()`](#module_f-message-form..getApplicationChoices) ⇒ <code>Array</code>
    * [`~_onScheduleTimeChange(e, val)`](#module_f-message-form.._onScheduleTimeChange)

<a name="module_f-message-form..getApplicationChoices"></a>

### `f-message-form~getApplicationChoices()` ⇒ <code>Array</code>
Получение опшнов в селекте претендентства

**Kind**: inner method of [<code>f-message-form</code>](#module_f-message-form)  
<a name="module_f-message-form.._onScheduleTimeChange"></a>

### `f-message-form~\_onScheduleTimeChange(e, val)`
Обработчик изменнеия значения в поле отправить в

**Kind**: inner method of [<code>f-message-form</code>](#module_f-message-form)  

| Param | Type |
| --- | --- |
| e | <code>Event</code> | 
| val | <code>String</code> | 

