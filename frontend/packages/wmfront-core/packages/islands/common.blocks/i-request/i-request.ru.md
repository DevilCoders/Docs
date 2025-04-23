# i-request
Блок для работы с http-запросами. Сам по себе пользовательского функционала не имеет, использовать нужно различные его модификации.

### Модификаторы блока
Модификатор | Описание | Допустимые значения
--- | --- | ---
`type` | Тип | [ajax](#ajax): Простой AJAX-запрос <br>[jsonrpc](#jsonrpc): AJAX-запросы по протоколу JSON-RPC.


В общем виде работа с блоком осуществляется следующим образом:

 1. С помощью `BEM.create(name, params)` создаем инстанс блока нужной модификации.
 1. В момент создания вторым параметром передаем базовые параметры инстанса.
 1. Используем полученный инстанс многократно, при необходимости переопределяя/доопределяя базовые параметры для конкретного запроса.


### Параметры

<table class="params_table">
    <thead>
        <tr>
            <th rowspan="2">Название</th>
            <th rowspan="2">Тип</th>
            <th rowspan="2">Общие</th>
            <th rowspan="2">type_ajax</th>
            <th colspan="2">type_jsonrpc</th>
            <th rowspan="2">Описание</th>
        </tr>
        <tr>
            <th>на одном домене</th>
            <th>кроссдоменные</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>cache</td>
            <td>Boolean</td>
            <td>false</td>
            <td>true</td>
            <td colspan="2"></td>
            <td>Нужно ли кэшировать результаты запросов.</td>
        </tr>
        <tr>
            <td>cacheGroup</td>
            <td>String</td>
            <td>"default"</td>
            <td></td>
            <td colspan="2"></td>
            <td>Название для кэш-группы. Если не переопределять, все инстансы будут кэшировать в одно хранилище.</td>
        </tr>
        <tr>
            <td>cacheSize</td>
            <td>Number</td>
            <td>100</td>
            <td></td>
            <td colspan="2"></td>
            <td>Сколько результатов хранить в кэш-группе.</td>
        </tr>
        <tr>
            <td>callbackCtx</td>
            <td>Object</td>
            <td>this</td>
            <td></td>
            <td colspan="2"></td>
            <td>Контекст, с которым будут вызваны функции callback.</td>
        </tr>
        <tr>
            <td>retryCount</td>
            <td>Number</td>
            <td></td>
            <td>0</td>
            <td colspan="2">0</td>
            <td>Сколько раз переотправлять запрос при http-ошибках.</td>
        </tr>
        <tr>
            <td>retryInterval</td>
            <td>Number</td>
            <td></td>
            <td>2000</td>
            <td colspan="2">2000</td>
            <td>Интервал между повторными запросами при http-ошибках.</td>
        </tr>
        <tr>
            <td>type</td>
            <td>String</td>
            <td></td>
            <td>"GET"</td>
            <td>"POST"</td>
            <td>"GET"</td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>dataType</td>
            <td>String</td>
            <td></td>
            <td>"jsonp"</td>
            <td>"json"</td>
            <td>"jsonp"</td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>timeout</td>
            <td>Number</td>
            <td></td>
            <td>20000</td>
            <td colspan="2">20000</td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>url</td>
            <td>String</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>data</td>
            <td>Object|String</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>contentType</td>
            <td>String</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>jsonp</td>
            <td>String</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>jsonpCallback</td>
            <td>String</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>xhrFields</td>
            <td>String</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>см. <a href="http://api.jquery.com/jQuery.ajax/">jQuery.ajax</a></td>
        </tr>
        <tr>
            <td>paramsToSettings</td>
            <td>String[]</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>По умолчанию проверяются только часто используемые параметры метода jQuery.ajax (см. выше).
            Если передаются дополнительные параметры, то их названия следует явно указать в paramsToSettings.</td>
        </tr>
        <tr>
            <td>onError</td>
            <td>Function</td>
            <td></td>
            <td></td>
            <td colspan="2"></td>
            <td>Callback на неудачное завершение запроса.</td>
        </tr>
    </tbody>
</table>
<small>* Все параметры можно переопределить в момент создания инстанса, либо в момент отправки запроса.</small>


<a name="ajax"></a>
### Простые AJAX-запросы

```javascript
// Создаем инстанс и определяем базовые параметры
var ajax = BEM.create("i-request_type_ajax", {
    url: "http://site.ru/data",
    cache: false
});

// Передаем данные, оба колбэка, доопределяем/переопределяем параметры
ajax.get(

    // data
    {
        obj: "table",
        prop: "color"
    },

    // success
    function (data) { console.log(data); },

    // error (можно не передавать)
    function (data) { console.log(data); },

    // params (можно не передавать)
    {                   // Только для этого запроса
        retryCount: 3   // три раза переспросим сервер
        cache: true     // и закешируем
    }
);

// Передаем данные, один колбек, доопределяем параметр callbackCtx
// Параметры retryCount и cache скинулись к исходным (0 и false)
ajax.get({ obj: "car", prop: "speed" }, successClbk, { callbackCtx: this });
```

<a name="jsonrpc"></a>
### AJAX-запросы по протоколу JSON-RPC

**API** (i-request_type_jsonrpc.js).

Эта модификация блока `i-request` предназначена для отправки запросов и уведомлений по протоколу JSON-RPC 2.0.

* Общая информация: [en.wikipedia.org/wiki/JSON-RPC](en.wikipedia.org/wiki/JSON-RPC)
* Спецификация (2.0): [jsonrpc.org/specification](jsonrpc.org/specification)

Особенности:

* Скрипт используется клиентской стороной.
* Группировка не поддерживается, запросы отправляются по одному.
* Транспорт: HTTP ($.ajax).
* Тип: POST (на одном домене), GET + jsonp (кроссдоменные).
* По умолчанию кэширование выключено.

Блок не имеет DOM-представления, его нужно прописать в каком-нибудь `deps.js`, который учитывается при сборке страницы.

Создается динамически в других блоках с помощью `BEM.create('i-request_type_jsonrpc', {...})`. Вторым аргументом передаются параметры блока.

Получив инстанс этого блока, его можно многократно использовать, вызывая методы `get` и `notify`.

Метод `get` наследуется от базового блока и, соответственно, имеет такую же сигнатуру. Важно лишь понимать, что запрос за данными идет по протоколу JSON-RPC. К примеру функции callback, которые передаются в метод, не про HTTP, а про JSON-RPC, то есть, если с кодом 200 пришла JSON-RPC ошибка, будет вызван onError.

Для конкретного вызова параметры, заданные в момент создания блока, можно переопределить.

#### Методы
##### notify([request], [params])
'Уведомление': тип запроса, специфичный для JSON-RPC. Сервер может не подтверждать получение такого запроса.

`request {Object}` – Объект с полями `method` и `params`.
`params {Object}` – Параметры блока.

```javascript
// Создаем инстанс и определяем базовые параметры
var jsonrpc = BEM.create("i-request_type_jsonrpc", {
    url: "/servlet/rpc",
    callbackCtx: this
});

// Значимые поля: method и params. Все остальное будет удалено.
jsonrpc.get(
    {
        method: "doSmth",
        params: ["with", "this", "stuff"]
    },
    function (data) {...},
    function (data) {...}
);

jsonrpc.get(
    { method: "getSuperSecretInfo", params: {pass: "123"} },
    successFn,
    { url: "https://secret.ru/rpc" }
);
```
