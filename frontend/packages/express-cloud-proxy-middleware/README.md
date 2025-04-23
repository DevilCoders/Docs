# express-cloud-proxy-middleware

Express middleware для проксирования запросов на адреса, которые можно задать в конфиге. Предполагается, что в конфиге
мы описываем сервис и запросы, которые он посылает к нам и которые мы должны проксировать в него. С помощью конфига
задается шаблон `url` для проксирования и `url` на который нужно проксировать запрос. Перед проксированием запроса, из
заголовка `cookie` удаляются куки `Session_id`, `sessionid2` и `yc_session`


Внутри для проксирования используется middleware [`http-proxy-middleware`](https://github.com/chimurai/http-proxy-middleware/tree/v0.21.0)

## Пример:

В примере ниже задаётся конфиг, который устанавливает, что все запросы вида `/__external_request/someService/ping` будут проксироваться
на `http://someservice.com/ping`, а запросы вида `/_external/someService/entity/([a-b0-9])`, где `([a-b0-9])` это некторый идентификатор,
будут проксироваться на `http://someservice.com/entity/get/$1`, где `$1` это плейсхолдер для подстановки идентификатора.

```javascript
const proxyMiddleware = require('express-cloud-proxy-middleware');
const express = require('express');
const app = express();

app.use(proxyMiddleware({
    services: [
        {
            host: 'http://someservice.com',
            routes: {
                [String.raw`/_external_request/someService/ping`]: '/ping',
                [String.raw`/_external/someService/entity/([a-b0-9])`]: 'http://someservice.com/entity/get/$1',
            },
            getHeaders(req) {
                return {
                    'Some-Additional-Header': 'You-need-this-header',
                    'Some-Header-From-Req': req.placeForHeaders.header
                };
            }
        }
    ]
}));
app.listen(3000);
```

## Опции
- **`services`**: массив с конфигурациями для сервисов с настройками для проксирования.
- **`logger`**: логгер. Если не указан, то будет использоваться console.
- **`getRequestLogger`**: фунция получения логгера для каждого запроса. Если не указана, то используется logger.

## Опции сервиса
- **`host`**: хост на который нужно проксировать запросы описанные в `routes`.
- **`routes`**: объект с входящими `url` и `url` на которые нужно осуществлять проксирование. Ключ и значение могут быть регулярными выражениями.
- **`getHeaders`**: функция, которая возвращает объект с заголовками, которыми будет расширен проксируемый запрос.
- **`prepareHost`**: функция, которая позваляет обработать строку хоста перед началом проксирования.
- **`proxyMiddlewareParams`**: объект с параметрами для `http-proxy-middleware`.
