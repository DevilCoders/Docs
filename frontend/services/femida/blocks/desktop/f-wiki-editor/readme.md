<a name="module_f-wiki-editor"></a>

## f-wiki-editor ⇐ <code>BEM.DOM</code>
Поле редактирования wiki с превью
Модификатор preview {Boolean} (отображение preview)

**Extends**: <code>BEM.DOM</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-wiki-editor',
    mods: {
        size: 'm',
        preview: Boolean
    },
    text: 'text', // Вики разметка
    wiki: '…' // Викиформатированный html
    name: 'name',
    placeholder: 'placeholder',
    buttons: [
       ['h2', 'h3'],
       ['bold', 'italic', 'underline', 'strikethrough'],
       ['ul', 'ol'],
       ['indent', 'outdent'],
       ['quote', 'separator', 'link', 'picture', 'code', 'table', 'color']
    ], // Array
    rows: 10 // Number
}
```

* [f-wiki-editor](#module_f-wiki-editor) ⇐ <code>BEM.DOM</code>
    * [`~val([value])`](#module_f-wiki-editor..val) ⇒ <code>String</code>
    * [`~wiki([value], reset)`](#module_f-wiki-editor..wiki) ⇒ <code>String</code>
    * [`~checkPreview()`](#module_f-wiki-editor..checkPreview)
    * [`"preview" (mode)`](#event_preview)

<a name="module_f-wiki-editor..val"></a>

### `f-wiki-editor~val([value])` ⇒ <code>String</code>
Значение поля

**Kind**: inner method of [<code>f-wiki-editor</code>](#module_f-wiki-editor)  

| Param | Type |
| --- | --- |
| [value] | <code>String</code> | 

<a name="module_f-wiki-editor..wiki"></a>

### `f-wiki-editor~wiki([value], reset)` ⇒ <code>String</code>
Викиформатированное значение поля

**Kind**: inner method of [<code>f-wiki-editor</code>](#module_f-wiki-editor)  

| Param | Type | Description |
| --- | --- | --- |
| [value] | <code>String</code> |  |
| reset | <code>Boolean</code> | сбросить эталонный текст |

<a name="module_f-wiki-editor..checkPreview"></a>

### `f-wiki-editor~checkPreview()`
Обновляет викиформатированное превью, если оно устарело

**Kind**: inner method of [<code>f-wiki-editor</code>](#module_f-wiki-editor)  
<a name="event_preview"></a>

### `"preview" (mode)`
**Kind**: event emitted by [<code>f-wiki-editor</code>](#module_f-wiki-editor)  

| Param | Type |
| --- | --- |
| mode | <code>Boolean</code> | 

