<a name="module_f-subscriptions-list"></a>

## f-subscriptions-list ⇐ <code>fa-pagable-collection</code>
Список подписок

**Extends**: <code>fa-pagable-collection</code>  
**Author**: olgakozlova  
**Example**  
```js
{
    block: 'f-subscriptions-list',
    js: {
        collection: {
            page: Number,
            query: {…}
        }
    }
}
```

* [f-subscriptions-list](#module_f-subscriptions-list) ⇐ <code>fa-pagable-collection</code>
    * [`~page()`](#module_f-subscriptions-list..page)
    * [`~setQuery(params)`](#module_f-subscriptions-list..setQuery)
    * [`~_onPageChange()`](#module_f-subscriptions-list.._onPageChange)
    * [`"results Успешная загрузка коллекции" (total)`](#event_results Успешная загрузка коллекции)
    * [`"page" (page)`](#event_page)
    * [`"error Ошибка загрузки списка"`](#event_error Ошибка загрузки списка)

<a name="module_f-subscriptions-list..page"></a>

### `f-subscriptions-list~page()`
**Kind**: inner method of [<code>f-subscriptions-list</code>](#module_f-subscriptions-list)  
**See**: fa-pagable-collection.page  
<a name="module_f-subscriptions-list..setQuery"></a>

### `f-subscriptions-list~setQuery(params)`
Поставить поисковый запрос в коллекцию

**Kind**: inner method of [<code>f-subscriptions-list</code>](#module_f-subscriptions-list)  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 

<a name="module_f-subscriptions-list.._onPageChange"></a>

### `f-subscriptions-list~\_onPageChange()`
**Kind**: inner method of [<code>f-subscriptions-list</code>](#module_f-subscriptions-list)  
**See**: fa-pagable-collection._onPageChange  
<a name="event_results Успешная загрузка коллекции"></a>

### `"results Успешная загрузка коллекции" (total)`
**Kind**: event emitted by [<code>f-subscriptions-list</code>](#module_f-subscriptions-list)  

| Param | Type | Description |
| --- | --- | --- |
| total | <code>Number</code> | полное кличество результатов |

<a name="event_page"></a>

### `"page" (page)`
Переключение страницы
cancelable

**Kind**: event emitted by [<code>f-subscriptions-list</code>](#module_f-subscriptions-list)  

| Param | Type |
| --- | --- |
| page | <code>Number</code> | 

<a name="event_error Ошибка загрузки списка"></a>

### `"error Ошибка загрузки списка"`
**Kind**: event emitted by [<code>f-subscriptions-list</code>](#module_f-subscriptions-list)  
