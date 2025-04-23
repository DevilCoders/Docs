Интерфейс и memcached реализация кэширования, совместимая с [Resource](https://github.yandex-team.ru/vertis/resource).

## Использование с resource

```javascript
ServiceResource = Resource.create()
    .setCache(new Cache(options));
```

## Реализации

### memcached

```javascript
new Cache({
    type : memcached,

    options: {
        // сервер или список серверов (массивом строк) memcached
        // https://github.com/3rd-Eden/memcached#server-locations
        servers : '127.0.0.1:11281',

        // TTL ключа, если не указано иное в методе set
        defaultKeyTTL : 60000,

        // поколение ключей
        // можно изменять для инвалидации ключей в бэкэнде
        // без прямого взаимодействия с бэкэндом
        generation : 1,
        
        // Таймаут в мс на чтение из memcached
        readTimeout : 50,

        // Опции memcached
        // https://github.com/3rd-Eden/memcached#options
        memcachedOptions : {}
    }
});
```

Также в `options.zipkinTracer` можно передедать экземпляр `zipkin.Tracer`,
тогда `memcached` будет обернут в `zipkin-instrumentation-memcached`. 

## Интерфейс

Реализации должны соответствовать общему интерфейсу.

### Cache(options)

Конструктор.

Аргументы:
* `Object options` – хэш специфичных для реализации опций.

### Cache#set(key, value, ttl)

Аргументы:
* `String key` – ключ, любая непустая строка. Нормализацию ключа, если это необходимо бэкэнду, метод должен выполнять сам.
* `String value` – любой объект без циклических ссылок. Приведение к формату пригодному для бэкэнда метод должен выполнять сам.
* `Number [ttl]` – время жизни ключа. Если не передано или 0, то остается на усмотрение реализации или бэкэнда.

Метод ничего не возвращает, в случае ошибок может писать сообщения об ошибках стандартными методами, но не бросать исключения.

### Cache#get(key)

Аргументы:
* `String key` – ключ, любая непустая строка. Нормализацию ключа, если это необходимо бэкэнду, метод должен выполнять сам.

Метод возвращает Promise с  интерфейсом Promise/A+.

В случае успеха Promise разрешается объектом, имеющим следующую структуру:

```javascript
{
    // результат в том виде, в котором он был передан методу set
    data : result,

    // метаинформация
    meta : {
        time : {
            // время выполнения операции
            total : operationExecutionTime
        },

        // маркер, всегда true
        cache : true
    }
}
```

В случае ошибки Promise отменяется с ошибкой `Cache.Error` (подкласс [Terror](http://npm.im/terror)).

Коды ошибок:
* `READ_ERROR` – ошибка получения ключа из бэкэнда.
* `KEY_NOT_FOUND` –  ключ не существует.
* `OPERATION_TIMEOUT` – превышено допустимое время выполнения операции.
* `JSON_PARSING_FAILED` – если значение ключа десериализуется из json и произошла ошибка десериализации.
