<a name="module_f-problems-list"></a>

## f-problems-list ⇐ <code>fa-pagable-collection</code>
Список задач

**Extends**: <code>fa-pagable-collection</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-problems-list',
    js: {
        collection: {
            page: Number,
            query: {…}
        }
    }
}
```

* [f-problems-list](#module_f-problems-list) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-problems-list..page)
    * [`~clear()`](#module_f-problems-list..clear)
    * [`~setQuery(params)`](#module_f-problems-list..setQuery)
    * [`~_onPageChange()`](#module_f-problems-list.._onPageChange)
    * [`"assign" (model)`](#event_assign)
    * [`"unassign" (model)`](#event_unassign)
    * [`"page" (page)`](#event_page)
    * [`"results Успешная загрузка коллекции" (total)`](#event_results Успешная загрузка коллекции)
    * [`"error Ошибка загрузки списка"`](#event_error Ошибка загрузки списка)

<a name="module_f-problems-list..page"></a>

### `f-problems-list~page()`
**Kind**: inner method of [<code>f-problems-list</code>](#module_f-problems-list)  
**See**: fa-pagable-collection.page  
<a name="module_f-problems-list..clear"></a>

### `f-problems-list~clear()`
Очистить таблицу
Удаляет все элементы из коллекции
Удаляет результаты поиска
Ставит модификатор empty

**Kind**: inner method of [<code>f-problems-list</code>](#module_f-problems-list)  
<a name="module_f-problems-list..setQuery"></a>

### `f-problems-list~setQuery(params)`
Поставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-problems-list</code>](#module_f-problems-list)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-problems-list.._onPageChange"></a>

### `f-problems-list~\_onPageChange()`
**Kind**: inner method of [<code>f-problems-list</code>](#module_f-problems-list)  
**See**: fa-pagable-collection._onPageChange  
<a name="event_assign"></a>

### `"assign" (model)`
Задать задачу

**Kind**: event emitted by [<code>f-problems-list</code>](#module_f-problems-list)  

| Param | Type |
| --- | --- |
| model | <code>Problem</code> | 

<a name="event_unassign"></a>

### `"unassign" (model)`
Убрать задачу

**Kind**: event emitted by [<code>f-problems-list</code>](#module_f-problems-list)  

| Param | Type |
| --- | --- |
| model | <code>Problem</code> | 

<a name="event_page"></a>

### `"page" (page)`
Переключение страницы
cancelable

**Kind**: event emitted by [<code>f-problems-list</code>](#module_f-problems-list)  

| Param | Type |
| --- | --- |
| page | <code>Number</code> | 

<a name="event_results Успешная загрузка коллекции"></a>

### `"results Успешная загрузка коллекции" (total)`
**Kind**: event emitted by [<code>f-problems-list</code>](#module_f-problems-list)  

| Param | Type | Description |
| --- | --- | --- |
| total | <code>Number</code> | полное кличество результатов |

<a name="event_error Ошибка загрузки списка"></a>

### `"error Ошибка загрузки списка"`
**Kind**: event emitted by [<code>f-problems-list</code>](#module_f-problems-list)  
