# express-informer-middleware

Express middleware для создания endpoint'a для получения данных информеров из [АПИ Бункера](https://wiki.yandex-team.ru/verstka/tools/bunker/api/).
Предлагается для использования в паре с компонентом `Informer`, который необходимо будет настроить на поход в данный endpoint.
С помощью конфига задается хост `bunker API` и версия запрашиваемых данных.

**Внимание!**
Для работы с продакшен-АПИ Бункера не забудьте заказать сетевой доступ до `bunker-api.yandex.net` от своего сетевого макроса.

## Пример:

В примере конфиг задается с помощи функции от `req` (сделано для примера, можно передавать обычным объектом), который устанавливает, что 
- созданный endpoint будет ходить в АПИ Бункера для разработки и тестирования (для его использования не требуются сетевые доступы)
- будет браться последняя версия данных (в том числе данные, неопубликованные в Бункере) 

```javascript
const expressInformerMiddleware = require('express-informer-middleware');
const express = require('express');
const app = express();

app.use('/informer-route', expressInformerMiddleware(req => ({
    bunkerApiHost: 'bunker-api-dot.yandex.net',
    version: 'latest',
})));

app.listen(3000);
```

Данный пример эквивалентен следующему:

```javascript
const expressInformerMiddleware = require('express-informer-middleware');
const express = require('express');
const app = express();

app.use('/informer-route', expressInformerMiddleware({
    bunkerApiHost: 'bunker-api-dot.yandex.net',
    version: 'latest',
}));

app.listen(3000);
```

## Опции
- **`bunkerApiHost`**(необязательный): хост АПИ Бункера. По-умолчанию будет использоваться `bunker-api.yandex.net` – хост АПИ для production, для использования которого необходимо заказать сетевой доступ.
- **`version`**(необязательный): [версия данных в АПИ Бункера](https://wiki.yandex-team.ru/verstka/tools/bunker/api/#m-get-params). По-умолчанию будет использоваться `stable` – последняя опубликованная версия.