<a name="module_f-vacancies-table"></a>

## f-vacancies-table ⇐ <code>fa-pagable-collection</code>
Таблица со списком вакансий

**Extends**: <code>fa-pagable-collection</code>  
**Author**: annvas  
**Example**  
```js
{
    block: 'f-vacancies-table',
    js: {
        collection: {
        page: '1'
    },
    fields: [
        {type: 'name'},
        {type: 'status'},
        {type: 'recruiters'},
        {type: 'hiring_manager'},
        {type: 'head'},
        {type: 'startrek_key'},
        {type: 'customers'}
    ]
}
```

* [f-vacancies-table](#module_f-vacancies-table) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-vacancies-table..page)
    * [`~setSearchParams(params)`](#module_f-vacancies-table..setSearchParams)
    * [`~clear()`](#module_f-vacancies-table..clear)
    * [`"page" (page)`](#event_page)

<a name="module_f-vacancies-table..page"></a>

### `f-vacancies-table~page()`
**Kind**: inner method of [<code>f-vacancies-table</code>](#module_f-vacancies-table)  
**See**: fa-pagable-collection.page  
<a name="module_f-vacancies-table..setSearchParams"></a>

### `f-vacancies-table~setSearchParams(params)`
Проставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-vacancies-table</code>](#module_f-vacancies-table)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-vacancies-table..clear"></a>

### `f-vacancies-table~clear()`
Очистить таблицу
Удаляет все элементы из коллекции
Удаляет результаты поиска
Ставит модификатор empty

**Kind**: inner method of [<code>f-vacancies-table</code>](#module_f-vacancies-table)  
<a name="event_page"></a>

### `"page" (page)`
Переключение страницы
cancelable

**Kind**: event emitted by [<code>f-vacancies-table</code>](#module_f-vacancies-table)  

| Param | Type |
| --- | --- |
| page | <code>Number</code> | 

