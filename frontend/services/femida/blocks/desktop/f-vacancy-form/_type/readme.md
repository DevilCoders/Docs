<a name="module_f-vacancy-form"></a>

## f-vacancy-form ⇐ <code>BEM.DOM</code>
**Extends:** <code>BEM.DOM</code>  
**Author:** olgakozlova  
**Example**  
```js
// Форма досоздания
{
    block: 'f-vacancy-form',
    mods: {type: 'after-create'},
    js: {data: {structure: {…}, data: {…}}}
    data: {structure: {…}, data: {…}}
}
```
<a name="module_f-vacancy-form.._serializeHook"></a>

### `f-vacancy-form~_serializeHook(e, data)`
Дописывает в данные значения остальных полей для корректной работы ручки редактирования

**Kind**: inner method of <code>[f-vacancy-form](#module_f-vacancy-form)</code>  

| Param | Type |
| --- | --- |
| e | <code>Event</code> | 
| data | <code>Object</code> | 


<a name="module_f-vacancy-form_type_create"></a>

## f-vacancy-form_type_create ⇐ <code>f-vacancy-form</code>
**Extends:** <code>f-vacancy-form</code>  
**Author:** dezmound  

* [f-vacancy-form_type_create](#module_f-vacancy-form_type_create) ⇐ <code>f-vacancy-form</code>
    * [`~destruct()`](#module_f-vacancy-form_type_create..destruct)
    * [`~updateMetaFields(data)`](#module_f-vacancy-form_type_create..updateMetaFields)

<a name="module_f-vacancy-form_type_create..destruct"></a>

### `f-vacancy-form_type_create~destruct()`
**Kind**: inner method of <code>[f-vacancy-form_type_create](#module_f-vacancy-form_type_create)</code>  
<a name="module_f-vacancy-form_type_create..updateMetaFields"></a>

### `f-vacancy-form_type_create~updateMetaFields(data)`
Перерисовывает предзаполняемые поля по переданным данным

**Kind**: inner method of <code>[f-vacancy-form_type_create](#module_f-vacancy-form_type_create)</code>  
**Access:** public  

| Param | Type |
| --- | --- |
| data | <code>Object</code> | 

