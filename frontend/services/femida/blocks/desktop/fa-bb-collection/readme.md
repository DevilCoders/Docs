<a name="module_fa-bb-collection"></a>

## fa-bb-collection ⇐ <code>fa-bb</code>
Имплементация представления для Backbone.Collection

**Extends**: <code>fa-bb</code>  
**Author**: ertema  

* [fa-bb-collection](#module_fa-bb-collection) ⇐ <code>fa-bb</code>
    * [`~_itemBlockMods`](#module_fa-bb-collection.._itemBlockMods)
    * [`~_itemBlockParams`](#module_fa-bb-collection.._itemBlockParams)
    * [`~_initItem`](#module_fa-bb-collection.._initItem)
    * [`~fetch()`](#module_fa-bb-collection..fetch) ⇒ <code>Promise</code>
    * [`~reset()`](#module_fa-bb-collection..reset) ⇒ <code>\*</code>
    * [`~set()`](#module_fa-bb-collection..set) ⇒ <code>\*</code>
    * [`~add()`](#module_fa-bb-collection..add) ⇒ <code>\*</code>
    * [`~bindToCollection()`](#module_fa-bb-collection..bindToCollection) ⇒ <code>\*</code>
    * *[`~_getItems()`](#module_fa-bb-collection.._getItems)*
    * [`~_getCid(elem)`](#module_fa-bb-collection.._getCid) ⇒ <code>String</code>

<a name="module_fa-bb-collection.._itemBlockMods"></a>

### `fa-bb-collection~\_itemBlockMods`
Модификаторы блока модели

**Kind**: inner property of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection.._itemBlockParams"></a>

### `fa-bb-collection~\_itemBlockParams`
Дополнительные параметры блока модели

**Kind**: inner property of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection.._initItem"></a>

### `fa-bb-collection~\_initItem`
Инициализация блока элемента

**Kind**: inner property of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection..fetch"></a>

### `fa-bb-collection~fetch()` ⇒ <code>Promise</code>
Загрузка данных модели

**Kind**: inner method of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection..reset"></a>

### `fa-bb-collection~reset()` ⇒ <code>\*</code>
Замена моделей коллекции

**Kind**: inner method of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection..set"></a>

### `fa-bb-collection~set()` ⇒ <code>\*</code>
Обновление моделей коллекции

**Kind**: inner method of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection..add"></a>

### `fa-bb-collection~add()` ⇒ <code>\*</code>
добавление моделей в коллекцию

**Kind**: inner method of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection..bindToCollection"></a>

### `fa-bb-collection~bindToCollection()` ⇒ <code>\*</code>
Привязка события к коллекции

**Kind**: inner method of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection.._getItems"></a>

### *`fa-bb-collection~\_getItems()`*
Должен возвращать все DOM элементы коллекции

**Kind**: inner abstract method of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
<a name="module_fa-bb-collection.._getCid"></a>

### `fa-bb-collection~\_getCid(elem)` ⇒ <code>String</code>
Получает cid элемента

**Kind**: inner method of [<code>fa-bb-collection</code>](#module_fa-bb-collection)  
**Preserve**:   

| Param | Type |
| --- | --- |
| elem | <code>Element</code> | 

