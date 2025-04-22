bem-protocol
============
Протокол реализует общение между клиентом и сервером в терминах BEMa. Соответственно реализация состоит из двух блоков: `i-request_type_bem`, `i-response_type_bem`. Первый блок отвечает за отправку запроса на клиенте, второй — за ответ сервера. `i-request_type_bem` для отправки запроса использует `i-request_type_ajax`.

Пример запроса:

```js
BEM
    .create('i-request_type_bem', {
        url: '/yandsearch',
        ctx: this
    })
    .block('b-page_type_search', function(response) {
        BEM.DOM.update(this.findBlockInside('b-page-wrap').domElem, response.html);
    })
    .block('b-search', function(response) {
        this
            .findBlockInside('b-search')
            .findBlockInside('b-form-input')
            .val(response.params.val || '');
    })
    .get({ text: 'bmw', rpt: 'image' }, function() {
        this.trigger('change', { page: 'search' });
    });
```

В этом примере мы хотим получить в ответ от сервера два блока: `b-page_type_search` и `b-search`. У каждого блока есть свой `callback`, `response` которого изолирован. Т.е. запрошенный блок никак не может обратиться к информации другого запрошенного блока. Контекст выполнения задается при создании объекта (`ctx: this`).

В результате выполнения данного кода отправится AJAX-запрос по адресу `/yandsearch?text=bmw&rpt=image&format=json&request=...`, где `request` — строковое представление объекта, содержащего все запрашиваемые блоки:

```js
JSON.stringify({ block: 'b-page_type_search', block: 'b-search' })
```

Серверная часть реализует простейший механизм контроля доступа (ACL) для запрашиваемых блоков. Поэтому прежде, чем получить какой-либо ответ от сервера, необходимо добавить ключи запрашиваемых блоков в специальный список.

```js
blocks['i-response_type_bem:push']('b-page_type_search', 'b-search')
```

Ключи блоков — не что иное, как название функции в приватных наблонах:

```js
blocks['b-page_type_search'] = function(data) {
    return {
       block: 'b-page'
       // ...
    }
}
```

На результат выполнения этого блока накладывается BEMHTML шаблоны и возвращается объект типа:

```js
{
    cnt: '...',
    blocks: [
        {
            block: 'b-page_type_search',
            html: '...',
            params: {},
            mods: {}
        },
        {
            block: 'b-search',
            html: '...',
            params: {}
        }
    ]
}
```

Ответ сервера превращается в строку с помощью `JSON.stringify()` и отправляется клиенту.
