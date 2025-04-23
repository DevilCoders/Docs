<a name="module_f-dialog-trigger"></a>

## f-dialog-trigger ⇐ <code>BEM.DOM</code>
Блок открывающий диалоговое окно

**Extends**: <code>BEM.DOM</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-dialog-trigger',
    mods: {
        dialog: 'modal' // или popup
        switcher: 'menu-item' // или button
    },
    dialog: { // Дополнительный BEMJSON диалогового окна
        content: 'text'
    }
}
```

* [f-dialog-trigger](#module_f-dialog-trigger) ⇐ <code>BEM.DOM</code>
    * [`~setContent(content)`](#module_f-dialog-trigger..setContent)
    * [`~getDialogElem()`](#module_f-dialog-trigger..getDialogElem) ⇒ <code>jQuery</code>

<a name="module_f-dialog-trigger..setContent"></a>

### `f-dialog-trigger~setContent(content)`
Задает содержимое диалогового окна

**Kind**: inner method of [<code>f-dialog-trigger</code>](#module_f-dialog-trigger)  

| Param | Type |
| --- | --- |
| content | <code>Object</code> \| <code>String</code> | 

<a name="module_f-dialog-trigger..getDialogElem"></a>

### `f-dialog-trigger~getDialogElem()` ⇒ <code>jQuery</code>
Возвращает элемент диалогового окна

**Kind**: inner method of [<code>f-dialog-trigger</code>](#module_f-dialog-trigger)  
