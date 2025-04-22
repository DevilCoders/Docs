<a name="module_f-publication-action"></a>

## f-publication-action ⇐ <code>BEM.DOM</code>
**Extends**: <code>BEM.DOM</code>  
**Author**: dezmound  

* [f-publication-action](#module_f-publication-action) ⇐ <code>BEM.DOM</code>
    * [`~loadForm()`](#module_f-publication-action..loadForm) ⇒ <code>Promise.&lt;void&gt;</code>
    * [`~_drawForm(data)`](#module_f-publication-action.._drawForm) ⇒ <code>Object</code>
    * [`~_renderForm(bemJson)`](#module_f-publication-action.._renderForm)
    * [`~_onFormLoadError(e)`](#module_f-publication-action.._onFormLoadError)

<a name="module_f-publication-action..loadForm"></a>

### `f-publication-action~loadForm()` ⇒ <code>Promise.&lt;void&gt;</code>
Загружает и перерисовывает форму

**Kind**: inner method of [<code>f-publication-action</code>](#module_f-publication-action)  
<a name="module_f-publication-action.._drawForm"></a>

### `f-publication-action~\_drawForm(data)` ⇒ <code>Object</code>
Возвращает BEMJSON для формы рекомендации

**Kind**: inner method of [<code>f-publication-action</code>](#module_f-publication-action)  

| Param | Type |
| --- | --- |
| data | <code>Object</code> | 

<a name="module_f-publication-action.._renderForm"></a>

### `f-publication-action~\_renderForm(bemJson)`
Рендерит содержимое формы

**Kind**: inner method of [<code>f-publication-action</code>](#module_f-publication-action)  

| Param | Type |
| --- | --- |
| bemJson | <code>Object</code> | 

<a name="module_f-publication-action.._onFormLoadError"></a>

### `f-publication-action~\_onFormLoadError(e)`
Обработчик ошибки загрузки формы

**Kind**: inner method of [<code>f-publication-action</code>](#module_f-publication-action)  

| Param | Type |
| --- | --- |
| e | <code>Event</code> | 

