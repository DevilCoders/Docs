<a name="module_/lib/date/seconds-to-time"></a>

## /lib/date/seconds-to-time ⇒ <code>String</code>
Разбивка секунд на часы/минуты/секунды в удобочитаемый формат, например
138  -> "02:18";
7541 -> "2:05:41";
Есть возможность указать разделитель вторым аргументом (по умолчанию двоеточие :)

**Returns**: <code>String</code> - Строковое представление числа секунд в удобочитаемом формате  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| sec | <code>Number</code> |  | число секунд |
| [separator] | <code>String</code> | <code>&quot;:&quot;</code> | разделитель |

