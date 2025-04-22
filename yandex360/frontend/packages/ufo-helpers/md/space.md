<a name="module_/lib/space"></a>

## /lib/space
Модуль генерации строкового представления размера файла.

Экспортирует объект с двумя методами генерации строки места, занимаемого файлом.

Методы различаются только форматом возвращаемого значения - один генерирует готовую строку,
другой генерирует объект с числом и единицами измерения.


* [/lib/space](#module_/lib/space)
    * _static_
        * [.getSpaceObject(bytes, units, separator, [params])](#module_/lib/space.getSpaceObject) ⇒ <code>SpaceObject</code>
        * [.getSpaceString(bytes, units, separator, [params])](#module_/lib/space.getSpaceString) ⇒ <code>String</code>
    * _inner_
        * [~SpaceObject](#module_/lib/space..SpaceObject) : <code>Object</code>

<a name="module_/lib/space.getSpaceObject"></a>

### /lib/space.getSpaceObject(bytes, units, separator, [params]) ⇒ <code>SpaceObject</code>
Возвращает объект с двумя полями: number - числовое представление и unit - единица измерения размера файла.

**Kind**: static method of <code>[/lib/space](#module_/lib/space)</code>  
**Returns**: <code>SpaceObject</code> - объект размера файла  

| Param | Type | Description |
| --- | --- | --- |
| bytes | <code>Number</code> | размер файла в байтах |
| units | <code>Array</code> | массив локализованных единиц измерения [байт, КБ, МБ, ГБ, ТБ] |
| separator | <code>String</code> | локализованный разделитель между целой и дробной частями числа |
| [params] | <code>Object</code> | объект с необязательными параметрами |
| [params.length] | <code>Number</code> | желаемая длина числа в размере файла без учёта разделителя.                                      Длина целой части может быть больше этого значения, но если длина меньше,                                      то на дробную часть останется (params.length - длина целой части) символов. |
| [params.precision] | <code>Number</code> | максимальное число знаков после запятой в представлении размера файла |

<a name="module_/lib/space.getSpaceString"></a>

### /lib/space.getSpaceString(bytes, units, separator, [params]) ⇒ <code>String</code>
Возвращает строковое представление размера файла.

**Kind**: static method of <code>[/lib/space](#module_/lib/space)</code>  
**Returns**: <code>String</code> - строковое представление размера файла  

| Param | Type | Description |
| --- | --- | --- |
| bytes | <code>Number</code> | размер файла в байтах |
| units | <code>Array</code> | массив локализованных единиц измерения [байт, КБ, МБ, ГБ, ТБ] |
| separator | <code>String</code> | локализованный разделитель между целой и дробной частями числа |
| [params] | <code>Object</code> | объект с необязательными параметрами |
| [params.length] | <code>Number</code> | желаемая длина числа в размере файла без учёта разделителя.                                      Длина целой части может быть больше этого значения, но если длина меньше,                                      то на дробную часть останется (params.length - длина целой части) символов. |
| [params.precision] | <code>Number</code> | максимальное число знаков после запятой в представлении размера файла |

<a name="module_/lib/space..SpaceObject"></a>

### /lib/space~SpaceObject : <code>Object</code>
**Kind**: inner typedef of <code>[/lib/space](#module_/lib/space)</code>  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| number | <code>String</code> | числовое представление размера файла без единиц измерения |
| unit | <code>String</code> | единицы измерения |

