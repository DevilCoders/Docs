## Functions

<dl>
<dt><a href="#sortedIndex">sortedIndex(array, item, comparator)</a> ⇒ <code>number</code></dt>
<dd><p>возвращает индекс, на который нужно поставить новый элемент, чтобы массив оставался отсортированным</p>
</dd>
</dl>

## Typedefs

<dl>
<dt><a href="#Comparator">Comparator</a> ⇒ <code>number</code></dt>
<dd><p>сравнивает аргументы из возвращает -1 или 1</p>
</dd>
</dl>

<a name="sortedIndex"></a>

## sortedIndex(array, item, comparator) ⇒ <code>number</code>
возвращает индекс, на который нужно поставить новый элемент, чтобы массив оставался отсортированным

**Kind**: global function  
**Returns**: <code>number</code> - индекс для нового элемента  

| Param | Type | Description |
| --- | --- | --- |
| array | <code>array</code> | массив, в который происходит вставка |
| item | <code>object</code> | новый элемент |
| comparator | <code>[Comparator](#Comparator)</code> | функция, возвращающая число меньше 0, если второе число должно идти после первого, и число больше 0 иначе |

<a name="Comparator"></a>

## Comparator ⇒ <code>number</code>
сравнивает аргументы из возвращает -1 или 1

**Kind**: global typedef  

| Type |
| --- |
| <code>object</code> | 
| <code>object</code> | 

