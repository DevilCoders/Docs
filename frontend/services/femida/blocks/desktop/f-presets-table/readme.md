<a name="module_f-presets-table"></a>

## f-presets-table ⇐ <code>fa-pagable-collection</code>
Таблица со списком пресетов задач

**Extends**: <code>fa-pagable-collection</code>  
**Author**: tsadekova  

* [f-presets-table](#module_f-presets-table) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-presets-table..page)
    * [`~setQuery(page)`](#module_f-presets-table..setQuery)
    * [`~clear()`](#module_f-presets-table..clear)
    * [`"results Успешная загрузка коллекции" (total)`](#event_results Успешная загрузка коллекции)
    * [`"error Ошибка загрузки списка"`](#event_error Ошибка загрузки списка)

<a name="module_f-presets-table..page"></a>

### `f-presets-table~page()`
**Kind**: inner method of [<code>f-presets-table</code>](#module_f-presets-table)  
**See**: fa-pagable-collection.page  
<a name="module_f-presets-table..setQuery"></a>

### `f-presets-table~setQuery(page)`
Проставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-presets-table</code>](#module_f-presets-table)  

| Param | Type |
| --- | --- |
| page | <code>Object</code> | 

<a name="module_f-presets-table..clear"></a>

### `f-presets-table~clear()`
Очистить таблицу
Удаляет все элементы из коллекции
Удаляет результаты поиска
Ставит модификатор empty

**Kind**: inner method of [<code>f-presets-table</code>](#module_f-presets-table)  
<a name="event_results Успешная загрузка коллекции"></a>

### `"results Успешная загрузка коллекции" (total)`
**Kind**: event emitted by [<code>f-presets-table</code>](#module_f-presets-table)  

| Param | Type | Description |
| --- | --- | --- |
| total | <code>Number</code> | полное кличество результатов |

<a name="event_error Ошибка загрузки списка"></a>

### `"error Ошибка загрузки списка"`
**Kind**: event emitted by [<code>f-presets-table</code>](#module_f-presets-table)  
