### Привязка нескольких обработчиков
В данный момент к одному событию можно привязать только один обработчик.

В случае, если потребуется привязывать несколько обработчиков, можно воспользоваться следующим кодом:
```javascript
bindBackendEvent: function(backendEvent, prefix, newEvent) {
    this.evetnsByType['prefix' + newEvent] = backendEvent;
    return function(event, callback) {
        var backendEvent = evetnsByType[prefix + '.' + event];
        this.callbackStorage[backendEvent].push(callback);
        if(!this._listeners[backendEvent]) {
            this._listeners[backendEvent] = function() {
                this.callbackStorage[backendEvent].map(function(value) {
                    value.apply(this, arguments);
                })
            };
        }
    }
}
```
