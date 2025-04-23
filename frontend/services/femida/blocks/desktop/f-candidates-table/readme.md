<a name="module_f-candidates-table"></a>

## f-candidates-table ⇐ <code>fa-pagable-collection</code>
Список кандидатов

**Extends**: <code>fa-pagable-collection</code>  
**Author**: annvas  

* [f-candidates-table](#module_f-candidates-table) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-candidates-table..page)
    * [`~setSearchText(text)`](#module_f-candidates-table..setSearchText)
    * [`~setQuery(params)`](#module_f-candidates-table..setQuery)
    * [`~clear()`](#module_f-candidates-table..clear)
    * [`"error Ошибка загрузки списка"`](#event_error Ошибка загрузки списка)

<a name="module_f-candidates-table..page"></a>

### `f-candidates-table~page()`
**Kind**: inner method of [<code>f-candidates-table</code>](#module_f-candidates-table)  
**See**: fa-pagable-collection.page  
<a name="module_f-candidates-table..setSearchText"></a>

### `f-candidates-table~setSearchText(text)`
Проставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-candidates-table</code>](#module_f-candidates-table)  

| Param | Type |
| --- | --- |
| text | <code>String</code> | 

<a name="module_f-candidates-table..setQuery"></a>

### `f-candidates-table~setQuery(params)`
Проставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-candidates-table</code>](#module_f-candidates-table)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-candidates-table..clear"></a>

### `f-candidates-table~clear()`
Очистить таблицу
Удаляет все элементы из коллекции
Удаляет результаты поиска
Ставит модификатор empty

**Kind**: inner method of [<code>f-candidates-table</code>](#module_f-candidates-table)  
<a name="event_error Ошибка загрузки списка"></a>

### `"error Ошибка загрузки списка"`
**Kind**: event emitted by [<code>f-candidates-table</code>](#module_f-candidates-table)  
