<a name="module_s-field_type_attachments"></a>

## s-field_type_attachments ⇐ <code>s-field</code>
Файлы

**Extends:** <code>s-field</code>  
**Author:** ertema  
**Example**  
```js
{
    block: 's-field',
    mods: {type: 'attachments'},
    name: 'files',
    field: {
        uploadUrl: '/api/upload/',
        uploadMethod: 'POST',
        maxFiles: 10,
        headers: {
            token: 'value'
        },
        accept: 'png'
    }
}
```

* [s-field_type_attachments](#module_s-field_type_attachments) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_attachments..val) ⇒ <code>Array</code>
    * [`~append(value)`](#module_s-field_type_attachments..append)
    * [`~getControl()`](#module_s-field_type_attachments..getControl) ⇒ <code>BEM</code>

<a name="module_s-field_type_attachments..val"></a>

### `s-field_type_attachments~val(value)` ⇒ <code>Array</code>
Значение

**Kind**: inner method of <code>[s-field_type_attachments](#module_s-field_type_attachments)</code>  
**Returns**: <code>Array</code> - — возвращается массив строк  

| Param | Type |
| --- | --- |
| value | <code>Array</code> | 

<a name="module_s-field_type_attachments..append"></a>

### `s-field_type_attachments~append(value)`
Дополнение уже существующего значения

**Kind**: inner method of <code>[s-field_type_attachments](#module_s-field_type_attachments)</code>  

| Param | Type |
| --- | --- |
| value | <code>Array</code> | 

<a name="module_s-field_type_attachments..getControl"></a>

### `s-field_type_attachments~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_attachments](#module_s-field_type_attachments)</code>  

<a name="module_s-field_type_checkbox"></a>

## s-field_type_checkbox ⇐ <code>s-field</code>
Чекбокс

**Extends:** <code>s-field</code>  
**Author:** annvas  
**Example**  
```js
{
    block: 's-field',
    mods: {type: 'checkbox'},
    name: 'check',
    field: {
        value: 'N',
        values: {
            checked: 'Y',
            unchecked: 'N'
        },
        label: 'label'
    }
}
```

* [s-field_type_checkbox](#module_s-field_type_checkbox) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_checkbox..val) ⇒ <code>String</code>
    * [`~getControl()`](#module_s-field_type_checkbox..getControl) ⇒ <code>BEM</code>
    * [`~_onReset()`](#module_s-field_type_checkbox.._onReset)

<a name="module_s-field_type_checkbox..val"></a>

### `s-field_type_checkbox~val(value)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_checkbox](#module_s-field_type_checkbox)</code>  
**Returns**: <code>String</code> - — возвращается строка  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>String</code> | — передаётся строка |

<a name="module_s-field_type_checkbox..getControl"></a>

### `s-field_type_checkbox~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_checkbox](#module_s-field_type_checkbox)</code>  
<a name="module_s-field_type_checkbox.._onReset"></a>

### `s-field_type_checkbox~_onReset()`
Обработка reset формы

**Kind**: inner method of <code>[s-field_type_checkbox](#module_s-field_type_checkbox)</code>  

<a name="module_s-field_type_custom-date"></a>

## s-field_type_custom-date ⇐ <code>s-field</code>
Поле ввода даты без использования календаря

**Extends:** <code>s-field</code>  
**Author:** olgakozlova  
<a name="module_s-field_type_custom-date..val"></a>

### `s-field_type_custom-date~val(value)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_custom-date](#module_s-field_type_custom-date)</code>  
**Returns**: <code>String</code> - — возвращается строка вида YYYY-MM-DD  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>String</code> | — передаётся строка вида YYYY-MM-DD |


<a name="module_s-field_type_date"></a>

## s-field_type_date ⇐ <code>s-field</code>
Поле ввода дат

**Extends:** <code>s-field</code>  
**Author:** annvas  

* [s-field_type_date](#module_s-field_type_date) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_date..val) ⇒ <code>String</code>
    * [`~getControl()`](#module_s-field_type_date..getControl) ⇒ <code>BEM</code>

<a name="module_s-field_type_date..val"></a>

### `s-field_type_date~val(value)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_date](#module_s-field_type_date)</code>  
**Returns**: <code>String</code> - — возвращается строка  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>String</code> | — передаётся строка |

<a name="module_s-field_type_date..getControl"></a>

### `s-field_type_date~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_date](#module_s-field_type_date)</code>  

<a name="module_s-field_type_datetime"></a>

## s-field_type_datetime ⇐ <code>s-field</code>
Поле ввода даты и времени

**Extends:** <code>s-field</code>  
**Author:** olgakozlova  

* [s-field_type_datetime](#module_s-field_type_datetime) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_datetime..val) ⇒ <code>String</code>
    * [`~getControl()`](#module_s-field_type_datetime..getControl) ⇒ <code>BEM</code>
    * [`~message()`](#module_s-field_type_datetime..message)
    * [`~_onControlChange(e, data)`](#module_s-field_type_datetime.._onControlChange)
    * [`~_getTooltip()`](#module_s-field_type_datetime.._getTooltip) ⇒ <code>BEM</code> &#124; <code>null</code>
    * [`~_format(value)`](#module_s-field_type_datetime.._format) ⇒ <code>String</code> &#124; <code>null</code>

<a name="module_s-field_type_datetime..val"></a>

### `s-field_type_datetime~val(value)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_datetime](#module_s-field_type_datetime)</code>  
**Returns**: <code>String</code> - — возвращается строка  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>String</code> | — передаётся строка |

<a name="module_s-field_type_datetime..getControl"></a>

### `s-field_type_datetime~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_datetime](#module_s-field_type_datetime)</code>  
<a name="module_s-field_type_datetime..message"></a>

### `s-field_type_datetime~message()`
**Kind**: inner method of <code>[s-field_type_datetime](#module_s-field_type_datetime)</code>  
**See**: s-base.message  
<a name="module_s-field_type_datetime.._onControlChange"></a>

### `s-field_type_datetime~_onControlChange(e, data)`
Обработчик изменения контрола

**Kind**: inner method of <code>[s-field_type_datetime](#module_s-field_type_datetime)</code>  

| Param | Type |
| --- | --- |
| e | <code>Event</code> | 
| data | <code>String</code> | 

<a name="module_s-field_type_datetime.._getTooltip"></a>

### `s-field_type_datetime~_getTooltip()` ⇒ <code>BEM</code> &#124; <code>null</code>
Возвращает блок tooltip с подсказкой о ошибке валидации

**Kind**: inner method of <code>[s-field_type_datetime](#module_s-field_type_datetime)</code>  
<a name="module_s-field_type_datetime.._format"></a>

### `s-field_type_datetime~_format(value)` ⇒ <code>String</code> &#124; <code>null</code>
Форматирует значение в формат, который принимает djangoDateTimeField

**Kind**: inner method of <code>[s-field_type_datetime](#module_s-field_type_datetime)</code>  

| Param | Type |
| --- | --- |
| value | <code>String</code> &#124; <code>null</code> | 


<a name="module_s-field_type_editor"></a>

## s-field_type_editor ⇐ <code>s-field</code>
**Extends:** <code>s-field</code>  
**Author:** ertema  
**Example**  
```js
{
    block: 's-field',
    mods: {type: 'editor'},
    name: 'name',
    placeholder: 'placeholder',
    field: {
        value: '//Italic//', // String
        buttons: [
           ['h2', 'h3'],
           ['bold', 'italic', 'underline', 'strikethrough'],
           ['ul', 'ol'],
           ['indent', 'outdent'],
           ['quote', 'separator', 'link', 'picture', 'code', 'table', 'color']
        ], // Array
        rows: 10 // Number
    }
}
```

* [s-field_type_editor](#module_s-field_type_editor) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_editor..val) ⇒ <code>String</code>
    * [`~getControl()`](#module_s-field_type_editor..getControl) ⇒ <code>BEM</code>

<a name="module_s-field_type_editor..val"></a>

### `s-field_type_editor~val(value)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_editor](#module_s-field_type_editor)</code>  

| Param | Type |
| --- | --- |
| value | <code>String</code> | 

<a name="module_s-field_type_editor..getControl"></a>

### `s-field_type_editor~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_editor](#module_s-field_type_editor)</code>  

<a name="module_s-field_type_femida-multiplesuggest"></a>

## s-field_type_femida-multiplesuggest ⇐ <code>s-field</code>
Мультиаджест с ручками фемиды

**Extends:** <code>s-field</code>  
**Author:** ertema  
**Example**  
```js
{
    block: 's-field',
    mods: {type: 'femida-multiplesuggest'},
    name: 'name',
    field: {
        value: [1],
        label_fields: {
            1: {caption: 'one'}
        },
        placeholder: 'text'
    }
}
```

* [s-field_type_femida-multiplesuggest](#module_s-field_type_femida-multiplesuggest) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_femida-multiplesuggest..val) ⇒ <code>Array</code>
    * [`~objectVal()`](#module_s-field_type_femida-multiplesuggest..objectVal) ⇒ <code>Array.&lt;Object&gt;</code>
    * [`~_onPlateRemove()`](#module_s-field_type_femida-multiplesuggest.._onPlateRemove)

<a name="module_s-field_type_femida-multiplesuggest..val"></a>

### `s-field_type_femida-multiplesuggest~val(value)` ⇒ <code>Array</code>
Значение

**Kind**: inner method of <code>[s-field_type_femida-multiplesuggest](#module_s-field_type_femida-multiplesuggest)</code>  
**Returns**: <code>Array</code> - — возвращается массив строк  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>Array</code> | — передаётся массив объектов |

<a name="module_s-field_type_femida-multiplesuggest..objectVal"></a>

### `s-field_type_femida-multiplesuggest~objectVal()` ⇒ <code>Array.&lt;Object&gt;</code>
Возвращает значение field, как массив объектов

**Kind**: inner method of <code>[s-field_type_femida-multiplesuggest](#module_s-field_type_femida-multiplesuggest)</code>  
**Access:** public  
<a name="module_s-field_type_femida-multiplesuggest.._onPlateRemove"></a>

### `s-field_type_femida-multiplesuggest~_onPlateRemove()`
Обработчик удаления плашки

**Kind**: inner method of <code>[s-field_type_femida-multiplesuggest](#module_s-field_type_femida-multiplesuggest)</code>  
**Emits**: <code>event:change</code>  

<a name="module_s-field_type_femida-multiplesugglect"></a>

## s-field_type_femida-multiplesugglect ⇐ <code>s-field</code>
Мультисагглект с ручками фемиды

**Extends:** <code>s-field</code>  
**Author:** gescbnet  
**Example**  
```js
{
    block: 's-field',
    mods: {type: 'femida-multiplesuggest'},
    name: 'name',
    field: {
        value: [1],
        label_fields: {
            1: {caption: 'one'}
        },
        placeholder: 'text'
    }
}
```

* [s-field_type_femida-multiplesugglect](#module_s-field_type_femida-multiplesugglect) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_femida-multiplesugglect..val) ⇒ <code>Array</code>
    * [`~objectVal()`](#module_s-field_type_femida-multiplesugglect..objectVal) ⇒ <code>Array.&lt;Object&gt;</code>
    * [`~_onRemovableDelete(event)`](#module_s-field_type_femida-multiplesugglect.._onRemovableDelete)

<a name="module_s-field_type_femida-multiplesugglect..val"></a>

### `s-field_type_femida-multiplesugglect~val(value)` ⇒ <code>Array</code>
Значение

**Kind**: inner method of <code>[s-field_type_femida-multiplesugglect](#module_s-field_type_femida-multiplesugglect)</code>  
**Returns**: <code>Array</code> - — возвращается массив строк  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>Array</code> | — передаётся массив объектов |

<a name="module_s-field_type_femida-multiplesugglect..objectVal"></a>

### `s-field_type_femida-multiplesugglect~objectVal()` ⇒ <code>Array.&lt;Object&gt;</code>
Возвращает значение field, как массив объектов

**Kind**: inner method of <code>[s-field_type_femida-multiplesugglect](#module_s-field_type_femida-multiplesugglect)</code>  
**Access:** public  
<a name="module_s-field_type_femida-multiplesugglect.._onRemovableDelete"></a>

### `s-field_type_femida-multiplesugglect~_onRemovableDelete(event)`
Обработчик клика на крестик плашки выбранного пункта саглекта

**Kind**: inner method of <code>[s-field_type_femida-multiplesugglect](#module_s-field_type_femida-multiplesugglect)</code>  

| Param | Type |
| --- | --- |
| event | <code>Event</code> | 


<a name="module_s-field_type_femida-suggest"></a>

## s-field_type_femida-suggest ⇐ <code>s-field</code>
Саджест с ручками фемиды

**Extends:** <code>s-field</code>  
**Author:** annvas  

* [s-field_type_femida-suggest](#module_s-field_type_femida-suggest) ⇐ <code>s-field</code>
    * [`~val(args)`](#module_s-field_type_femida-suggest..val) ⇒ <code>String</code>
    * [`~getControl()`](#module_s-field_type_femida-suggest..getControl) ⇒ <code>BEM</code>

<a name="module_s-field_type_femida-suggest..val"></a>

### `s-field_type_femida-suggest~val(args)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_femida-suggest](#module_s-field_type_femida-suggest)</code>  

| Param | Type |
| --- | --- |
| args | <code>Array.&lt;any&gt;</code> | 

<a name="module_s-field_type_femida-suggest..getControl"></a>

### `s-field_type_femida-suggest~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_femida-suggest](#module_s-field_type_femida-suggest)</code>  

<a name="module_s-field_type_multiplesuggest"></a>

## s-field_type_multiplesuggest ⇐ <code>s-field</code>
Мультиаджест

**Extends:** <code>s-field</code>  
**Author:** ertema  
<a name="module_s-field_type_multiplesuggest..val"></a>

### `s-field_type_multiplesuggest~val(value)` ⇒ <code>Array</code>
Значение

**Kind**: inner method of <code>[s-field_type_multiplesuggest](#module_s-field_type_multiplesuggest)</code>  
**Returns**: <code>Array</code> - — возвращается массив строк  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>Array</code> | — передаётся массив объектов |


<a name="module_s-field_type_plate-list"></a>

## s-field_type_plate-list ⇐ <code>s-field</code>
Список выбранных значений с кнопкой добавить

**Extends:** <code>s-field</code>  
**Author:** dezmound  
**Example**  
```js
{
    block: 's-field',
    mods: {type: 'plate-list'},
    name: 'name',
    field: {
        value: [1],
        label_fields: {
            1: {caption: 'one'}
        },
        placeholder: 'text'
    }
}
```

* [s-field_type_plate-list](#module_s-field_type_plate-list) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_plate-list..val) ⇒ <code>Array</code>
    * [`~objectVal()`](#module_s-field_type_plate-list..objectVal) ⇒ <code>Array.&lt;Object&gt;</code>
    * [`~_onPlateRemove()`](#module_s-field_type_plate-list.._onPlateRemove)

<a name="module_s-field_type_plate-list..val"></a>

### `s-field_type_plate-list~val(value)` ⇒ <code>Array</code>
Значение

**Kind**: inner method of <code>[s-field_type_plate-list](#module_s-field_type_plate-list)</code>  
**Returns**: <code>Array</code> - — возвращается массив строк  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>Array</code> | — передаётся массив объектов |

<a name="module_s-field_type_plate-list..objectVal"></a>

### `s-field_type_plate-list~objectVal()` ⇒ <code>Array.&lt;Object&gt;</code>
Возвращает значение field, как массив объектов

**Kind**: inner method of <code>[s-field_type_plate-list](#module_s-field_type_plate-list)</code>  
**Access:** public  
<a name="module_s-field_type_plate-list.._onPlateRemove"></a>

### `s-field_type_plate-list~_onPlateRemove()`
Обработчик удаления плашки

**Kind**: inner method of <code>[s-field_type_plate-list](#module_s-field_type_plate-list)</code>  
**Emits**: <code>event:change</code>  

<a name="module_s-field_type_range-choice"></a>

## s-field_type_range-choice ⇐ <code>s-field</code>
Два связанных choice, для выбора интервала
В min нельзя выбрать значение больше чем в max
В max нельзя выбрать значение меньше чем в min

**Extends:** <code>s-field</code>  
**Author:** ertema  
**Example**  
```js
{
    block: 's-field',
    mods: {type: 'range-choice'},
    name: 'name_min',
    field: {
        rangeId: 'name', // Для связи полей
        rangeType: 'min', // max для максимального поля, min для минимального
        value: '1', // String
        choices: [
            {label: 'Раз', value: '1'},
            {label: 'Два', value: '2'},
            {label: 'Три', value: '3'}
        ], // Array
        disabled: true, // Boolean
        required: true // Boolean
    }
},
{
    block: 's-field',
    mods: {type: 'range-choice'},
    name: 'name_min',
    field: {
        rangeId: 'name',
        rangeType: 'max',
        value: '3',
        choices: [
            {label: 'Раз', value: '1'},
            {label: 'Два', value: '2'},
            {label: 'Три', value: '3'}
        ]
    }
}
```

* [s-field_type_range-choice](#module_s-field_type_range-choice) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_range-choice..val) ⇒ <code>String</code>
    * [`~getControl()`](#module_s-field_type_range-choice..getControl) ⇒ <code>BEM</code>

<a name="module_s-field_type_range-choice..val"></a>

### `s-field_type_range-choice~val(value)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_range-choice](#module_s-field_type_range-choice)</code>  

| Param | Type |
| --- | --- |
| value | <code>String</code> | 

<a name="module_s-field_type_range-choice..getControl"></a>

### `s-field_type_range-choice~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_range-choice](#module_s-field_type_range-choice)</code>  

<a name="module_s-field_type_sort"></a>

## s-field_type_sort ⇐ <code>s-field</code>
Поле выбора сортировки

**Extends:** <code>s-field</code>  
**Author:** ertema  
**Example**  
```js
{
    block: 's-field',
    mods: {
        type: 'sort'
    },
    name: String,
    field: {
        choices: [
            {
                label: 'id',
                value: 'id'
            },
            …
        ],
        value: '-id',
        disabled: Boolean
    }
}
```
<a name="module_s-field_type_sort..val"></a>

### `s-field_type_sort~val([value])` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_sort](#module_s-field_type_sort)</code>  

| Param | Type |
| --- | --- |
| [value] | <code>String</code> | 


<a name="module_s-field_type_tags-cloud"></a>

## s-field_type_tags-cloud ⇐ <code>s-field</code>
**Extends:** <code>s-field</code>  
**Author:** annvas  

* [s-field_type_tags-cloud](#module_s-field_type_tags-cloud) ⇐ <code>s-field</code>
    * [`~val(value)`](#module_s-field_type_tags-cloud..val) ⇒ <code>String</code>
    * [`~getControl()`](#module_s-field_type_tags-cloud..getControl) ⇒ <code>BEM</code>

<a name="module_s-field_type_tags-cloud..val"></a>

### `s-field_type_tags-cloud~val(value)` ⇒ <code>String</code>
Значение

**Kind**: inner method of <code>[s-field_type_tags-cloud](#module_s-field_type_tags-cloud)</code>  

| Param | Type |
| --- | --- |
| value | <code>Array</code> | 

<a name="module_s-field_type_tags-cloud..getControl"></a>

### `s-field_type_tags-cloud~getControl()` ⇒ <code>BEM</code>
Базовый блок

**Kind**: inner method of <code>[s-field_type_tags-cloud](#module_s-field_type_tags-cloud)</code>  
