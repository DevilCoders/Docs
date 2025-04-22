<a name="module_f-attach-uploader"></a>

## f-attach-uploader ⇐ <code>BEM.DOM</code>
Загрузка вложений

**Extends**: <code>BEM.DOM</code>  
**Author**: ertema  
**Example**  
```js
{
    block: 'f-attach-uploader',
    mods: {
        size: 's',
        theme: 'normal'
    },
    js: {
        uploadUrl: '/api/upload/',
        uploadMethod: 'POST',
        parallelUploadLimit: 4,
        maxFiles: 50,
        maxSize: 1024 (bytes)
    },
    content: [
        {
            elem: 'file',
            elemMods: {state: 'success'},
            name: 'image',
            type: 'png',
            id: 64
        }
    ]
}
```

* [f-attach-uploader](#module_f-attach-uploader) ⇐ <code>BEM.DOM</code>
    * [`~remove(elem)`](#module_f-attach-uploader..remove)
    * [`~clear()`](#module_f-attach-uploader..clear)
    * [`~addFile(fileData)`](#module_f-attach-uploader..addFile) ⇒ <code>Sting</code>
    * [`"uploadStart"`](#event_uploadStart)
    * [`"uploadEnd"`](#event_uploadEnd)
    * [`"remove" (data)`](#event_remove)
    * [`"fileUploaded" (data)`](#event_fileUploaded)
    * [`"fileUploaded" (data)`](#event_fileUploaded)

<a name="module_f-attach-uploader..remove"></a>

### `f-attach-uploader~remove(elem)`
Удаляет переданный элемент файла из блока

**Kind**: inner method of [<code>f-attach-uploader</code>](#module_f-attach-uploader)  
**Emits**: [<code>remove</code>](#event_remove)  

| Param | Type |
| --- | --- |
| elem | <code>jQuery</code> | 

<a name="module_f-attach-uploader..clear"></a>

### `f-attach-uploader~clear()`
Удалить все файлы

**Kind**: inner method of [<code>f-attach-uploader</code>](#module_f-attach-uploader)  
<a name="module_f-attach-uploader..addFile"></a>

### `f-attach-uploader~addFile(fileData)` ⇒ <code>Sting</code>
Добавление уже загруженного файла в список

**Kind**: inner method of [<code>f-attach-uploader</code>](#module_f-attach-uploader)  
**Emits**: [<code>fileUploaded</code>](#event_fileUploaded)  

| Param | Type |
| --- | --- |
| fileData | <code>Object</code> | 

<a name="event_uploadStart"></a>

### `"uploadStart"`
Начало загрузки

**Kind**: event emitted by [<code>f-attach-uploader</code>](#module_f-attach-uploader)  
<a name="event_uploadEnd"></a>

### `"uploadEnd"`
Завершение загрузки

**Kind**: event emitted by [<code>f-attach-uploader</code>](#module_f-attach-uploader)  
<a name="event_remove"></a>

### `"remove" (data)`
Удаление вложения

**Kind**: event emitted by [<code>f-attach-uploader</code>](#module_f-attach-uploader)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.elem | <code>Object</code> | элемент файла |

<a name="event_fileUploaded"></a>

### `"fileUploaded" (data)`
Успешная загрузка файла

**Kind**: event emitted by [<code>f-attach-uploader</code>](#module_f-attach-uploader)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.elem | <code>Object</code> | элемент файла |
| data.response | <code>Object</code> | данные ответа |

<a name="event_fileUploaded"></a>

### `"fileUploaded" (data)`
Успешная загрузка файла

**Kind**: event emitted by [<code>f-attach-uploader</code>](#module_f-attach-uploader)  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>Object</code> |  |
| data.elem | <code>Object</code> | элемент файла |
| data.response | <code>Object</code> | данные ответа |

