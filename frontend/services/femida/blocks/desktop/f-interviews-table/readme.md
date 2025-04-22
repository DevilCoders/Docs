<a name="module_f-interviews-table"></a>

## f-interviews-table ⇐ <code>fa-pagable-collection</code>
Таблица со списком секций

**Extends**: <code>fa-pagable-collection</code>  
**Author**: annvas  

* [f-interviews-table](#module_f-interviews-table) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-interviews-table..page)
    * [`~clear()`](#module_f-interviews-table..clear)
    * [`~setQuery(params)`](#module_f-interviews-table..setQuery)
    * [`"page" (page)`](#event_page)
    * [`"error Ошибка загрузки списка"`](#event_error Ошибка загрузки списка)

<a name="module_f-interviews-table..page"></a>

### `f-interviews-table~page()`
**Kind**: inner method of [<code>f-interviews-table</code>](#module_f-interviews-table)  
**See**: fa-pagable-collection.page  
<a name="module_f-interviews-table..clear"></a>

### `f-interviews-table~clear()`
Очистить таблицу
Удаляет все элементы из коллекции
Удаляет результаты поиска
Ставит модификатор empty

**Kind**: inner method of [<code>f-interviews-table</code>](#module_f-interviews-table)  
<a name="module_f-interviews-table..setQuery"></a>

### `f-interviews-table~setQuery(params)`
Проставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-interviews-table</code>](#module_f-interviews-table)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="event_page"></a>

### `"page" (page)`
Переключение страницы
cancelable

**Kind**: event emitted by [<code>f-interviews-table</code>](#module_f-interviews-table)  

| Param | Type |
| --- | --- |
| page | <code>Number</code> | 

<a name="event_error Ошибка загрузки списка"></a>

### `"error Ошибка загрузки списка"`
**Kind**: event emitted by [<code>f-interviews-table</code>](#module_f-interviews-table)  
