# kotik-ws-proxy-middleware

Мидлвара для [kotik], реализующая проксирование websocket соединения. Является надстройкой над [@gemini-testing/http-proxy-middleware].

## Опции

### Опции http-proxy-middleware

Подробно описаны [тут][http-proxy-mw-opts].

### Опции kotik-ws-proxy-middleware

- `dumpScheme` - возможность выбрать схему проигрывания и сохранения дампов. Текущие поддерживаемые схемы: `sequence` и `strict`. Подробнее про данные схемы описано [тут](#Поддерживаемые-схемы-проигрывания-дампов). По умолчанию используется `sequence` схема;
- `strictReqOrder` - если ws и http запросы могут приходить в не строго заданном порядке, то рекомендуется выставить эту опцию в `false`. По умолчанию `true`;
- `wsInterceptClientMsg` - функция-перехватчик для фильтрации/модификации запроса до удаленного сервера. [Пример использования](#Модификация/фильтрация-запроса-до-удаленного-сервера);
- `wsInterceptServerMsg` - функция-перехватчик для фильтрации/модификации ответа от удаленного сервера. [Пример использования](#Модификация/фильтрация-ответа-от-удаленного-сервера);
- `wsGenerateClientMsgHash` - функция генерации уникального хэша запроса. [Пример использования](#Генерация-уникального-хэша-запроса-и-ответа);
- `wsGenerateServerMsgHash` - функция генерации уникального хэша ответа. [Пример использования](#Генерация-уникального-хэша-запроса-и-ответа);
- `middlewares` - возможность задекларировать свои мидлвары вместо используемых по умолчанию или добавить свою мидлвару к дефолтным. Подробнее описано [тут](#middlewares).

## Поддерживаемые схемы проигрывания дампов

### sequence

Данная схема последовательно проигрывает сообщения из дампа. Если у вас может изменяться порядок ws/http запросов, то необходимо использовать опцию `strictReqOrder: false`. Если у вас на проекте ws запросы отправляются параллельно, то ответы на них могут прийти в любом порядке. Соответственно, данная схема вам не подойдет и нужно использовать [strict](#strict).

### strict

Данная схема по сохраненному дампу строит структуру с запросами и ответами на них. Матчинг между запросом и ответом должен реализовать пользователь, используя функции `wsGenerateClientMsgHash` и `wsGenerateServerMsgHash`. Схема с запросом-ответом стабильнее, но нужно самостоятельно реализовать матчинг.

## Примеры использования

### Декларация мидлвары в конфиге котика

```js
const wsProxy = require('@yandex-int/kotik-ws-proxy-middleware');

...
{
    matcher: () => {...},
    handler: [
        {
            name: 'ws-proxy',
            fn: wsProxy('/some/url', {
                target: 'wss://echo.websocket.org',
                changeOrigin: true
            })
        }
    ]
}
...
```

### Модификация/фильтрация запроса до удаленного сервера

В данном примере текст (состоящий из букв) отправленный через проксю на удаленный сервер `wss://echo.websocket.org` будет перехвачен и приведен к верхнему регистру. Если в отправленном тексте отсутствуют буквы, то ничего на удаленный сервер отправлять не будем. Подробнее про обработчик `wsInterceptClientMsg` описано [в пакете @gemini-testing/http-proxy](https://github.com/gemini-testing/node-http-proxy):

```js
wsProxy('/some/url', {
    target: 'wss://echo.websocket.org',
    changeOrigin: true,
    wsInterceptClientMsg: (data) => {
        if (!/[a-zA-Zа-яА-Я]+/.test(data)) {
            return null;
        }

        return data.toUpperCase();
    }
});
```

### Модификация/фильтрация ответа от удаленного сервера

В данном примере текст отправленный от удаленного сервера `wss://echo.websocket.org` в нашу проксю будет перехвачен и дополнен строкой `_intercepted`. Если сервер ответил не строкой, то ничего на клиент отправлять не будем. Подробнее про обработчик `wsInterceptServerMsg` описано [в пакете @gemini-testing/http-proxy](https://github.com/gemini-testing/node-http-proxy)

```js
wsProxy('/some/url', {
    target: 'wss://echo.websocket.org',
    changeOrigin: true,
    wsInterceptServerMsg: (data) => {
        if (typeof data !== 'string') {
            return null;
        }

        return `${data}_intercepted`;
    }
});
```

### Генерация уникального хэша запроса и ответа

В данном примере для правильной работы схемы `strict` будем генерить одинаковый хэш для пары запроса и ответа.

```js
const crypto = require('crypto');

wsProxy('/some/url', {
    target: 'wss://echo.websocket.org',
    changeOrigin: true,
    wsGenerateClientMsgHash: (msg) => {
        return crypto.createHash('sha256').update(msg).digest('hex');
    },
    wsGenerateServerMsgHash: (msg) => {
        return crypto.createHash('sha256').update(msg).digest('hex');
    }
});
```

В итоге за счет того, что сервис echo.websocket.org отвечает такой же строкой, которую ему отправили, то хэш для запроса и ответа у нас будет одинаковый.

## Middlewares

Для данной мидлвары с помощью опций можно задекларировать свои мидлвары, которые предназначены для обработки websocket запросов. При этом эти мидлвары выполняются один раз до апгрейда соединения с http/https до ws/wss.

### Декларация мидлвар

Ничем не отличается от декларации мидлвар для котика и имеет следующий формат:

* **name** (required) `string` — название мидлвара
* **fn** (required) `function` — обработчик

Пример:
```js
wsProxy('/some/url', {
    target: 'wss://echo.websocket.org',
    changeOrigin: true,
    middlewares: [
        {
            name: 'my-awesome-middleware-1', fn: (wsReq, wsSocket, next, wsHead, wsProxy) => {...}
            name: 'my-awesome-middleware-2', fn: (wsReq, wsSocket, next, wsHead, wsProxy) => {...}
        }
    ]
})
```

### Примеры использования

#### Добавим вывод в консоль всех сообщений от клиента и от сервера

```js
wsProxy('/some/url', {
    target: 'wss://echo.websocket.org',
    changeOrigin: true,
    middlewares: [
        {
            name: 'ws-logger',
            fn: (wsParams, proxyReq, next) => {
                proxyReq.on('wsClientMsg', console.log);
                proxyReq.on('wsServerMsg', console.log);

                next();
            }
        }
    ]
})
```

### Примеры использования данной мидлвары

Чаты - https://github.yandex-team.ru/serp/chat.
Тестовый репозиторий - https://github.yandex-team.ru/dudkevich/kotik-ws-proxy-test

[kotik]: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/kotik
[@gemini-testing/http-proxy-middleware]: https://github.com/gemini-testing/http-proxy-middleware
[http-proxy-mw-opts]: https://github.com/gemini-testing/http-proxy-middleware#options
