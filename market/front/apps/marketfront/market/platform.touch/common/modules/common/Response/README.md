#Response.js

##API

####[Response] new Response([context])

```js
// Code of a module:
var Response = require('Response');
var http = require('http');

module.exports.requestData = function (url) {
    return new Response().listen(http.get(url));
};

// Usage:
module
    .requestData('ya.ru')
    .then(function (result) {
        // Processing result
    }, function (reason) {
        // Processing error
    });
```

###Отслеживание и изменение состояния объекта
####[Number] Response.STATE_PENDING = 0
####[Number] Response.STATE_RESOLVED = 1
####[Number] Response.STATE_REJECTED = 2

####[Response] Response#pending()
####[Response] Response#resolve()
####[Response] Response#reject()
####[Response] Response#clear()

####[Number] Response#state
####[Boolean] Response#isResolved

###Управление событиями
####[EventEmitter] Response#prototype
####[Response] Response#progress([progress])
####[Response] Response#final()

###Подписка на события:
####[EventEmitter] Response#prototype

####[String] Response#EVENT_RESOLVE = 'resolve'
####[String] Response#EVENT_REJECT = 'reject'
####[String] Response#EVENT_PROGRESS = 'progress'

####[Response] Response#notify([parent])
####[Response] Response#listen([response])
####[Response] Response#complete()
####[Response] Response#then([onResolve], [onReject], [onProgress])
####[Response] Response#onResolve(callback, [context])
####[Response] Response#onReject(callback, [context])
####[Response] Response#onProgress(callback, [context])
####[Response] Response#onResult(callback, [context])

###Контекст событий
####[Object|Null] Response#context
####[Response] Response#setContext([context])

###Обработка результатов
####[Array] Response#result
####[Error] Response#reason
####[Array|Function] Response#keys
####[Response] Response#setKeys([keys])
####[Array|Object|*] Response#map([keys])

###Пользовательские данные
####[*] Response#data
####[Response] Response#setData([data])

###Создание очереди
####[Queue] new Response.Queue([stack], [start])
####[Queue] Response.queue()
####[Queue] Response.strictQueue()

###Управление работой очереди
####[Array] Response.Queue#stack
####[Boolean] Response.Queue#stopped
####[*] Response.Queue#item

####[Queue] Response.Queue#start()
####[Queue] Response.Queue#stop()
####[Queue] Response.Queue#push()

###Подписка на события очереди
####[Response] Response.Queue#prototype
####[String] Response.Queue#EVENT_START = 'start'
####[String] Response.Queue#EVENT_STOP = 'stop'
####[String] Response.Queue#EVENT_RESOLVE_ITEM = 'resolveItem'
####[String] Response.Queue#EVENT_REJECT_ITEM = 'rejectItem'

####[Queue] Response.Queue#strict()
####[Queue] Response.Queue#onStart(callback, [context])
####[Queue] Response.Queue#onStop(callback, [context])
