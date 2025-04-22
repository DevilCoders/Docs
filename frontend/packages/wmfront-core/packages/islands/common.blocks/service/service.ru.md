# service

Блок предназначен для размещения на странице компонента сервиса. Визуально представлен следующими элементами или их различными комбинациями:

* названием сервиса (элемент `name`);
* URL сервиса (элемент `url`);
* иконкой сервиса (элемент `icon`);

_При использовании функциональности, представленной любым из этих элементов, его нужно подключить через зависимости._

API блока позволяет задать произвольное название и/или адрес сервису.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | --------------------- | -------- |
| [hoverable](#mods-hoverable)  | `yes` | BEMJSON | Декорирование блока при наведении курсором. |

### BEMJSON-поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [service](#fields-service)| String |Строковый ID сервиса, определенный в блоке [i-services](../common.blocks/i-services/__uri/i-services__uri.bemhtml.js).  |
| [name](#fields-name) | String | Название сервиса. |
| [icon](#fields-icon)| Boolean | Признак для отображения иконки сервиса. Значение по умолчанию: `true`.  |
| [iconMods](#fields-iconMods)| BEMJSON | Модификаторы иконки, передаваемые в блок [icon](../icon/icon.ru.md).
| [url](#fields-url) | String | Адрес страницы сервиса (базовая часть), переопределяющий значение по умолчанию из [i-services](../common.blocks/i-services/__uri/i-services__uri.bemhtml.js). Реализуется блоком [link](../link/link.ru.md).|
| [urlParams](#fields-url) | String | Дополнительные параметры для адреса сервиса, например, GET-параметры. |
| [urlAttrs](#fields-url) | BEMJSON | Атрибуты ссылки сервиса, передаются в блок [link](../link/link.ru.md). |
| [counter](#fields-counter) | String | Вспомогательное поле для добавления mousedown-счетчиков, значение которого помещается в атрибут `onmousedown` ссылки сервиса. |

## Подробнее

<a name="mods"></a>
### Модификаторы блока

<a name="mods-hoverable"></a>
#### Модификатор `hoverable`

Отвечает за декорирование блока при наведении курсором мыши.

Способы установки: BEMJSON.<br>
Допустимое значение: `yes`. 

_При использовании модификатора необходимо самостоятельно включить в зависимости блока модификатор `hoverable` в значении `yes`._


```js
{
    block: 'service',
    mods: {'hoverable': 'yes'},
    service: 'video',
    iconMods: {color: '56'}
}
```

<a name="fields"></a>
### BEMJSON-поля блока

<a name="fields-service"></a>
#### Поле `service`

Тип: `String`. <br>
Значение по умолчанию: –.

Определяет уникальный ID сервиса в Лего из блока [i-services](../common.blocks/i-services/__uri/i-services__uri.bemhtml.js). Позволяет получить различную информацию о сервисе для формирования блока со значениями по умолчанию:

* название сервиса и URL главной страницы сервиса, с учетом локализации, из [i-services](../common.blocks/i-services/__uri/i-services__uri.bemhtml.js) (список всех сервисов Яндекса);
* иконку сервиса из [service-icon](../common.blocks/service-icon/) (иконки всех сервисов Яндекса).

```js
{
    block: 'service',
    service: 'video',
    iconMods: {color: '56'}
}
```

<a name="fields-name"></a>
#### Поле `name`

Тип: `String`.<br>
Значение по умолчанию: `ctx.service`.

Определяет название сервиса. Значение поля передается в содержимое элемента `name`.

Возможные источники для значения (в порядке уменьшения приоритета):

* `ctx.name` – произвольное название;
* `this['i-services'].serviceName(service)` – название, полученное из блока [i-services](../common.blocks/i-services/__uri/i-services__uri.bemhtml.js);
* `ctx.service` – по умолчанию.

Сервис с произвольным названием:

```js
{
    block: 'service',
    service: 'video',
    name: 'Карты',
    iconMods: {color: '56'}
}
```

<a name="fields-icon"></a>
#### Поле `icon`

Тип: `Boolean`.<br>
Значение по умолчанию: `true`.

Определяет необходимость отображения иконки в блоке. По умолчанию будет установлена иконка сервиса из блока [service-icon](../common.blocks/service-icon/). Иконка помещается в элемент блока `icon`.

```js
{
    block: 'service',
    service: 'video'
}
```

Ссылка на сервис без иконки:

```js
{
    block: 'service',
    service: 'video',
    icon: false
}
```

<a name="fields-iconMods"></a>
#### Поле `iconMods`

Тип: `BEMJSON`.<br>
Значение по умолчанию: –.

Используется для передачи значений модификаторов элементу `icon`, если необходимо установить иконку сервиса с требуемыми параметрами (размер и цветность). Иконка нужного вида извлекается из блока [service-icon](../common.blocks/service-icon/) с помощью ID сервиса.

Блок `service-icon` требует указания модификатора `_self_40` или `_color_56` для отображения иконки. Если его не указать, иконка не появится. [Список поддерживаемых иконок для сервисов](../common.blocks/service-icon).

_Иконки сервисов с требуемыми параметрами необходимо добавить в зависимости блока_.

Ссылка на сервис с иконкой (цветная, размером 56х56 px):

```js
{
    block: 'service',
    service: 'video',
    iconMods: {color: '56'}
}
```

<a name="fields-url"></a>
#### Поле `url`

Тип: `String`.<br>
Значение по умолчанию: URL главной страницы сервиса (из блока [i-services](../common.blocks/i-services/__uri/i-services__uri.bemhtml.js)).

Определяет адрес ссылки сервиса (базовая часть).

Значения полей `url`, `urlParams`, `urlAttrs`, [counter](#fields-counter) передаются в содержимое элемента `url` и используются для формирования ссылки сервиса и ее атрибутов. Ссылка реализуется блоком [link](../link/link.ru.md).

Сервис с произвольным названием и адресом:

```js
{
    block: 'service',
    service: 'video',
    url: 'https://yandex.ru/images/',
    name: 'Карты',
    iconMods: {color: '56'}
}
```

Сервис с произвольным названием, адресом, атрибутами и GET-параметрами:

```js
{
    block: 'service',
    service: 'video',
    url: 'https://yandex.ru/images/',
    name: 'Карты',
    urlParams: '?text=simple',
    urlAttrs: {target: '_blank'}
}
```

<a name="fields-counter"></a>
#### Поле `counter`

Тип: `String`. <br>
Значение по умолчанию: –.

Определяет хелпер для добавления mousedown-счетчиков. Содержимое поля помещается в атрибут `onmousedown` ссылки сервиса [url](#fields-url).


```javascript
{
    block: 'service',
    service: 'video',
    url: 'https://yandex.ru/images/',
    name: 'Карты',
    urlParams: '?text=simple'
    urlAttrs: {
        // Например: counter: 'console.log("Send me to server")' счетчик с функцией логирования в консоль
        onmousedown: function(){/*...*/}
    }
}
```
