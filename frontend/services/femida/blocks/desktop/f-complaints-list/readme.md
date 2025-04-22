<a name="module_f-complaints-list"></a>

## f-complaints-list ⇐ <code>fa-pagable-collection</code>
Список жалоб

**Extends**: <code>fa-pagable-collection</code>  
**Author**: tsadekova  
**Example**  
```js
{
    block: 'f-complaints-list',
    js: {
        collection: {
            page: {Number}
        }
    }
}
```

* [f-complaints-list](#module_f-complaints-list) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-complaints-list..page)
    * [`~clear()`](#module_f-complaints-list..clear)
    * [`~setQuery(page)`](#module_f-complaints-list..setQuery)
    * [`"page" (page)`](#event_page)
    * [`"results Успешная загрузка коллекции" (total)`](#event_results Успешная загрузка коллекции)
    * [`"error Ошибка загрузки списка"`](#event_error Ошибка загрузки списка)

<a name="module_f-complaints-list..page"></a>

### `f-complaints-list~page()`
**Kind**: inner method of [<code>f-complaints-list</code>](#module_f-complaints-list)  
**See**: fa-pagable-collection.page  
<a name="module_f-complaints-list..clear"></a>

### `f-complaints-list~clear()`
Очистить таблицу
Удаляет все элементы из коллекции
Удаляет результаты поиска
Ставит модификатор empty

**Kind**: inner method of [<code>f-complaints-list</code>](#module_f-complaints-list)  
<a name="module_f-complaints-list..setQuery"></a>

### `f-complaints-list~setQuery(page)`
Проставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-complaints-list</code>](#module_f-complaints-list)  

| Param | Type |
| --- | --- |
| page | <code>Object</code> | 

<a name="event_page"></a>

### `"page" (page)`
Переключение страницы
cancelable

**Kind**: event emitted by [<code>f-complaints-list</code>](#module_f-complaints-list)  

| Param | Type |
| --- | --- |
| page | <code>Number</code> | 

<a name="event_results Успешная загрузка коллекции"></a>

### `"results Успешная загрузка коллекции" (total)`
**Kind**: event emitted by [<code>f-complaints-list</code>](#module_f-complaints-list)  

| Param | Type | Description |
| --- | --- | --- |
| total | <code>Number</code> | полное кличество результатов |

<a name="event_error Ошибка загрузки списка"></a>

### `"error Ошибка загрузки списка"`
**Kind**: event emitted by [<code>f-complaints-list</code>](#module_f-complaints-list)  
