<a name="module_/lib/is-browser-supported"></a>

## /lib/is-browser-supported ⇒ <code>Boolean</code>
Функция проверки поддержки браузера

**Returns**: <code>Boolean</code> - true если браузер поддерживается; false в противном случае  

| Param | Type | Description |
| --- | --- | --- |
| parsedAgent | <code>Object</code> | Объект с параметрами браузера, полученный от uatraits |
| unsupportedList | <code>Array</code> | Список неподдерживаемых браузеров. Элементы списка - объекты с полями, одноимёнными с полями в объекте с параметрами браузера, полученными от uatraits. Поле с версией сравнивается при помощи semver, остальные поля сравниваются на точное совпадение. |

**Example**  
```js
const isBrowserSupported = require('helpers/lib/is-browser-supported');
const UNSUPPORTED_BROWSERS = [
    { isMobile: false, BrowserName: 'MSIE', BrowserVersion: '<11' },
    { isMobile: false, BrowserName: 'Safari', BrowserVersion: '<7' },
    { BrowserName: 'Safari', OSName: 'Windows XP' },
    { isMobile: true, BrowserName: 'Chrome', BrowserVersion: '<5.2' }
];
const ua = new uatraits.Detector(...).detect(req.headers['user-agent']);
if (!isBrowserSupported(ua, UNSUPPORTED_BROWSERS)) { /* показать заглушку про устаревший браузер *\/ }
```
