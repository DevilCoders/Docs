<a name="module_f-publications-list"></a>

## f-publications-list ⇐ <code>fa-pagable-collection</code>
Список публикаций

**Extends**: <code>fa-pagable-collection</code>  
**Author**: dezmound  
**Example**  
```js
{
    block: 'f-publications-list',
    js: {
        collection: {
            page: Number,
            query: {…}
        }
    }
}
```

* [f-publications-list](#module_f-publications-list) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-publications-list..page)
    * [`~setQuery(params)`](#module_f-publications-list..setQuery)
    * [`~_onPageChange()`](#module_f-publications-list.._onPageChange)
    * [`"results Успешная загрузка коллекции" (total)`](#event_results Успешная загрузка коллекции)
    * [`"page" (page)`](#event_page)
    * [`"error Ошибка загрузки списка"`](#event_error Ошибка загрузки списка)

<a name="module_f-publications-list..page"></a>

### `f-publications-list~page()`
**Kind**: inner method of [<code>f-publications-list</code>](#module_f-publications-list)  
**See**: fa-pagable-collection.page  
<a name="module_f-publications-list..setQuery"></a>

### `f-publications-list~setQuery(params)`
Поставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-publications-list</code>](#module_f-publications-list)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-publications-list.._onPageChange"></a>

### `f-publications-list~\_onPageChange()`
**Kind**: inner method of [<code>f-publications-list</code>](#module_f-publications-list)  
**See**: fa-pagable-collection._onPageChange  
<a name="event_results Успешная загрузка коллекции"></a>

### `"results Успешная загрузка коллекции" (total)`
**Kind**: event emitted by [<code>f-publications-list</code>](#module_f-publications-list)  

| Param | Type | Description |
| --- | --- | --- |
| total | <code>Number</code> | полное кличество результатов |

<a name="event_page"></a>

### `"page" (page)`
Переключение страницы
cancelable

**Kind**: event emitted by [<code>f-publications-list</code>](#module_f-publications-list)  

| Param | Type |
| --- | --- |
| page | <code>Number</code> | 

<a name="event_error Ошибка загрузки списка"></a>

### `"error Ошибка загрузки списка"`
**Kind**: event emitted by [<code>f-publications-list</code>](#module_f-publications-list)  
