<a name="module_f-applications-table"></a>

## f-applications-table ⇐ <code>fa-pagable-collection</code>
Список претендентств

**Extends**: <code>fa-pagable-collection</code>  
**Author**: annvas  
**Example**  
```js
{
    block: 'f-applications-table',
    js: {
        collection: {
        page: '1',
        query: {
            sort: '-created'
            vacancy_id: 1
        }
    },
    fields: [
        {type: 'candidate'},
        {type: 'status'},
        {type: 'created_by'},
        {
            type: 'created',
            sort: true
        },
        {
            type: 'modified',
            sort: true
        },
        {type: 'actions'}
    ]
}
```

* [f-applications-table](#module_f-applications-table) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-applications-table..page)
    * [`~setSearchParams(params)`](#module_f-applications-table..setSearchParams)
    * [`~clear()`](#module_f-applications-table..clear)
    * [`~setSort(newSort)`](#module_f-applications-table..setSort)
    * [`"sort_changed" (data)`](#event_sort_changed)
    * [`"page" (page)`](#event_page)

<a name="module_f-applications-table..page"></a>

### `f-applications-table~page()`
**Kind**: inner method of [<code>f-applications-table</code>](#module_f-applications-table)  
**See**: fa-pagable-collection.page  
<a name="module_f-applications-table..setSearchParams"></a>

### `f-applications-table~setSearchParams(params)`
Проставить поисковый запрос или фильтр в коллекцию

**Kind**: inner method of [<code>f-applications-table</code>](#module_f-applications-table)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-applications-table..clear"></a>

### `f-applications-table~clear()`
Очистить таблицу
Удаляет все элементы из коллекции
Удаляет результаты поиска
Ставит модификатор empty

**Kind**: inner method of [<code>f-applications-table</code>](#module_f-applications-table)  
<a name="module_f-applications-table..setSort"></a>

### `f-applications-table~setSort(newSort)`
Изменение сортировки

**Kind**: inner method of [<code>f-applications-table</code>](#module_f-applications-table)  
**Emits**: [<code>sort\_changed</code>](#event_sort_changed)  

| Param | Type |
| --- | --- |
| newSort | <code>String</code> \| <code>Object</code> | 

<a name="event_sort_changed"></a>

### `"sort_changed" (data)`
Изменение сортировки

**Kind**: event emitted by [<code>f-applications-table</code>](#module_f-applications-table)  

| Param | Type |
| --- | --- |
| data | <code>Object</code> | 
| data.prev | <code>String</code> | 
| data.current | <code>String</code> | 

<a name="event_page"></a>

### `"page" (page)`
Переключение страницы
cancelable

**Kind**: event emitted by [<code>f-applications-table</code>](#module_f-applications-table)  

| Param | Type |
| --- | --- |
| page | <code>Number</code> | 

