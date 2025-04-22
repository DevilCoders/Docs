<a name="module_f-preset-problems-list"></a>

## f-preset-problems-list ⇐ <code>fa-bb-collection</code>
**Extends**: <code>fa-bb-collection</code>  
**Author**: tsadekova  
**Example**  
```js
{
    block: 'f-preset-problems-list',
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

* [f-preset-problems-list](#module_f-preset-problems-list) ⇐ <code>fa-bb-collection</code>
    * [`~setEmptyMessage(bemjson)`](#module_f-preset-problems-list..setEmptyMessage)
    * [`~findPresetProblemElem(target)`](#module_f-preset-problems-list..findPresetProblemElem) ⇒ <code>jQuery</code>
    * [`"sort-save" (ids)`](#event_sort-save)
    * [`"sort-cancel"`](#event_sort-cancel)

<a name="module_f-preset-problems-list..setEmptyMessage"></a>

### `f-preset-problems-list~setEmptyMessage(bemjson)`
Обновление сообщения для списка без задач

**Kind**: inner method of [<code>f-preset-problems-list</code>](#module_f-preset-problems-list)  

| Param | Type |
| --- | --- |
| bemjson | <code>Object</code> | 

<a name="module_f-preset-problems-list..findPresetProblemElem"></a>

### `f-preset-problems-list~findPresetProblemElem(target)` ⇒ <code>jQuery</code>
Найти DOM-элемент модели

**Kind**: inner method of [<code>f-preset-problems-list</code>](#module_f-preset-problems-list)  

| Param | Type |
| --- | --- |
| target | <code>Object</code> | 

<a name="event_sort-save"></a>

### `"sort-save" (ids)`
Сохранение сортировки

**Kind**: event emitted by [<code>f-preset-problems-list</code>](#module_f-preset-problems-list)  

| Param | Type |
| --- | --- |
| ids | <code>Array</code> | 

<a name="event_sort-cancel"></a>

### `"sort-cancel"`
Отмена сортировки

**Kind**: event emitted by [<code>f-preset-problems-list</code>](#module_f-preset-problems-list)  
