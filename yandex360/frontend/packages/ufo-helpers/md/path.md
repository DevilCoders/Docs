## Functions

<dl>
<dt><a href="#split">split(path)</a> ⇒ <code>Array.&lt;string&gt;</code></dt>
<dd><p>разбивает строку по слешам</p>
</dd>
<dt><a href="#basename">basename(path)</a> ⇒ <code>string</code></dt>
<dd><p>возвращает имя файла</p>
</dd>
<dt><a href="#extname">extname(path, [withDot])</a> ⇒ <code>string</code></dt>
<dd><p>возвращает расширение файла</p>
</dd>
<dt><a href="#normalize">normalize(path)</a> ⇒ <code>string</code></dt>
<dd><p>Приводит адрес к нормальному виду (убирает двойные слеши, вставляет в начало слеш)</p>
</dd>
<dt><a href="#segments">segments(path, fn)</a> ⇒ <code>string</code></dt>
<dd><p>применяет функцию преобразования строки к каждому из разделов пути, находящемуся между слешами</p>
</dd>
<dt><a href="#escape">escape(path)</a> ⇒ <code>string</code></dt>
<dd><p>применяет URL-кодировку к строке</p>
</dd>
<dt><a href="#unescape">unescape(path)</a> ⇒ <code>string</code></dt>
<dd><p>декодирует URL-кодировку</p>
</dd>
<dt><a href="#dirname">dirname(path)</a> ⇒ <code>string</code></dt>
<dd><p>Возвращает путь до папки, в которой находится файл</p>
</dd>
</dl>

<a name="split"></a>

## split(path) ⇒ <code>Array.&lt;string&gt;</code>
разбивает строку по слешам

**Kind**: global function  
**Returns**: <code>Array.&lt;string&gt;</code> - '/disk/path/to/folder/file.jpg' ⇒ ['disk', 'path', 'to', 'folder', 'file.jpg']  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь |

<a name="basename"></a>

## basename(path) ⇒ <code>string</code>
возвращает имя файла

**Kind**: global function  
**Returns**: <code>string</code> - '/disk/path/to/folder/file.jpg' ⇒ 'file.jpg'  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь |

<a name="extname"></a>

## extname(path, [withDot]) ⇒ <code>string</code>
возвращает расширение файла

**Kind**: global function  
**Returns**: <code>string</code> - 'file.ext' ⇒ 'ext', 'file.ext.jpg' ⇒ 'jpg', 'file' ⇒ '', 'file.' ⇒ ''  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь до файла |
| [withDot] | <code>boolean</code> | нужна ли точка в начале |

<a name="normalize"></a>

## normalize(path) ⇒ <code>string</code>
Приводит адрес к нормальному виду (убирает двойные слеши, вставляет в начало слеш)

**Kind**: global function  
**Returns**: <code>string</code> - 'disk///path/to/folder//file.jpg/' ⇒ '/disk/path/to/folder/file.jpg'  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь |

<a name="segments"></a>

## segments(path, fn) ⇒ <code>string</code>
применяет функцию преобразования строки к каждому из разделов пути, находящемуся между слешами

**Kind**: global function  
**Returns**: <code>string</code> - преобразованный путь  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь |
| fn | <code>function</code> | функция преобразования строки |

<a name="escape"></a>

## escape(path) ⇒ <code>string</code>
применяет URL-кодировку к строке

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь |

<a name="unescape"></a>

## unescape(path) ⇒ <code>string</code>
декодирует URL-кодировку

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь |

<a name="dirname"></a>

## dirname(path) ⇒ <code>string</code>
Возвращает путь до папки, в которой находится файл

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| path | <code>string</code> | путь до файла |

