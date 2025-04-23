<a name="module_f-categories"></a>

## f-categories ⇐ <code>fa-bb-collection</code>
Список категорий задач

**Extends**: <code>fa-bb-collection</code>  
**Author**: natamaki  

* [f-categories](#module_f-categories) ⇐ <code>fa-bb-collection</code>
    * [`~activeAllCategories()`](#module_f-categories..activeAllCategories)
    * [`~activeFoundCategories(data)`](#module_f-categories..activeFoundCategories)
    * [`~updateCollectionBySearchQuery(data)`](#module_f-categories..updateCollectionBySearchQuery)

<a name="module_f-categories..activeAllCategories"></a>

### `f-categories~activeAllCategories()`
Возвращает всем категориям активное состояние.

**Kind**: inner method of [<code>f-categories</code>](#module_f-categories)  
<a name="module_f-categories..activeFoundCategories"></a>

### `f-categories~activeFoundCategories(data)`
Выделяет найденные категории, как активные.

**Kind**: inner method of [<code>f-categories</code>](#module_f-categories)  

| Param | Type |
| --- | --- |
| data | <code>Array</code> | 

<a name="module_f-categories..updateCollectionBySearchQuery"></a>

### `f-categories~updateCollectionBySearchQuery(data)`
Обновляет коллекцию по поисковому запросу
Ручка всегда возвращает полный список категорий.
Продолжаем дергать на каждый поисковый запрос, вдруг во время сессии пользователя появились новые категории

**Kind**: inner method of [<code>f-categories</code>](#module_f-categories)  

| Param | Type |
| --- | --- |
| data | <code>Object</code> | 

