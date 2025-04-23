# DAO

Data access objects — a layer of abstraction between your api methods and a remote api.  

When calling an api method your api methods should only care about receiving a response,
not about the details of transfering the data to and from the backend.


## HTTP

Хочу ДАО!
```javascript
var dao = new HTTPDao(/* some configuration params */);
```
[Параметры в jsdoc](Http.js#L17-L27)


Сделай-ка мне http-запрос:

```javascript
dao.call('get', '/your/handle/', {data: 'data!'})
   .then(function(responseData) { /* yay! */ });
```

Сделай-ка мне запрос, но конкретно сейчас ретраиться не надо:
```javascript
dao.call('get', '/your/handle/', {data: 'data!'}, dao.cloneConfig().setMaxRetries(0))
   .then(function(responseData) { /* yay! */ });
```

### ApiFailCheck
При конфигурации ДАО можно указать метод, для проверки нужно ли сейчас поретраиться.  

Вызывается с логгером, полным ответом и попаршенным body.  
Должен вернуть falsey-значение когда всё хорошо или эксцепшен, когда нужно поретраиться.  
Эксцепшен нужно именно вернуть, а не кинуть (`return new Error('blah')`).
