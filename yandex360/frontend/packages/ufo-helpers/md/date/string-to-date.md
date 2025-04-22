<a name="module_/lib/date/string-to-date"></a>

## /lib/date/string-to-date ⇒ <code>Date</code>
Форматирует переданную строку даты в указанном формате в дату.
Формат по умолчанию: DD.MM.YYYY HH:mm

| Токен | Результат |
| ----- | --------- |
| M     | 1 2 ... 11 12 |
| MM    | 01 02 ... 11 12 |
| D     | 1 2 ... 30 31 |
| DD    | 01 02 ... 30 31 |
| YY    | 01 02 .. 16 17 |
| YYYY  | 2001 2002 ... 2016 2017 |
| H     | 1 2 ... 22 23 |
| HH    | 01 02 ... 22 23 |
| m     | 1 2 ... 58 59 |
| mm    | 01 02 ... 58 59 |
| s     | 1 2 ... 58 59 |
| ss    | 01 02 ... 58 59 |

**Returns**: <code>Date</code> - дата  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| dateString | <code>String</code> |  | строка даты |
| [format] | <code>String</code> | <code>&#x27;DD.MM.YYYY HH:mm&#x27;</code> | Формат даты, в соответствии со схемой выше |

