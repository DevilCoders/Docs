<a name="module_f-assignments-list"></a>

## f-assignments-list ⇐ <code>fa-bb-collection</code>
**Extends**: <code>fa-bb-collection</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-assignments-list',
    mods: {
        loading: Boolean,
        sort: Boolean
    },
    js: {
        collection: {…}, // Параметры коллекции
        models: […] // Модели в коллекции
    },
    emptyMessage: {…} // bemjson сообщения для списка без задач
}
```

* [f-assignments-list](#module_f-assignments-list) ⇐ <code>fa-bb-collection</code>
    * [`~_initActions()`](#module_f-assignments-list.._initActions)
    * [`~setEmptyMessage(bemjson)`](#module_f-assignments-list..setEmptyMessage)
    * [`~setInterview(interview)`](#module_f-assignments-list..setInterview)
    * [`~findAssignmentElem(target)`](#module_f-assignments-list..findAssignmentElem) ⇒ <code>jQuery</code>
    * [`"sort-save" (ids)`](#event_sort-save)
    * [`"sort-cancel"`](#event_sort-cancel)

<a name="module_f-assignments-list.._initActions"></a>

### `f-assignments-list~\_initActions()`
Инициализация экшнов

**Kind**: inner method of [<code>f-assignments-list</code>](#module_f-assignments-list)  
<a name="module_f-assignments-list..setEmptyMessage"></a>

### `f-assignments-list~setEmptyMessage(bemjson)`
Обновление сообщения для списка без задач

**Kind**: inner method of [<code>f-assignments-list</code>](#module_f-assignments-list)  

| Param | Type |
| --- | --- |
| bemjson | <code>Object</code> | 

<a name="module_f-assignments-list..setInterview"></a>

### `f-assignments-list~setInterview(interview)`
Обновление интервью

**Kind**: inner method of [<code>f-assignments-list</code>](#module_f-assignments-list)  

| Param | Type |
| --- | --- |
| interview | <code>Object</code> | 

<a name="module_f-assignments-list..findAssignmentElem"></a>

### `f-assignments-list~findAssignmentElem(target)` ⇒ <code>jQuery</code>
Найти DOM-элемент модели

**Kind**: inner method of [<code>f-assignments-list</code>](#module_f-assignments-list)  

| Param | Type |
| --- | --- |
| target | <code>Object</code> | 

<a name="event_sort-save"></a>

### `"sort-save" (ids)`
Сохранение сортировки

**Kind**: event emitted by [<code>f-assignments-list</code>](#module_f-assignments-list)  

| Param | Type |
| --- | --- |
| ids | <code>Array</code> | 

<a name="event_sort-cancel"></a>

### `"sort-cancel"`
Отмена сортировки

**Kind**: event emitted by [<code>f-assignments-list</code>](#module_f-assignments-list)  
