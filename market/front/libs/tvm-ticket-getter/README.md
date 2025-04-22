# TVM Ticket Getter [![npm version](https://badger.yandex-team.ru/npm/@yandex-market/tvm-ticket-getter/version.svg)](https://npm.yandex-team.ru/@yandex-market/tvm-ticket-getter)
Модуль для запроса и переодического обновления TVM тикета.

## Интерфейс
* ```createTicketGetter({object} config): TicketGetter``` – создание объекта TicketGetter
    * ```config``` – формат описан в Параметры конфига
* ```TicketGetter#start()``` – запрос тикета и переодическое обновление
* ```TicketGetter#stop()``` – остановка обновления  
* ```TicketGetter#getTicket()``` – вернуть последний полученный тикет
* ```TicketGetter#setLogger(logger)``` – включить логирование через logger
    * ```logger``` имеет сигнатуру ```logger#log({string} message, {string} level)```
* ```event 'ticket'``` новый полученный тикет
* ```event 'error'``` произошедшая ошибка
## Параметры конфига
```javascript
{
    // интервал между перезапросами в случае ошибки, в мс
    requestDelay: 2000,
    // интервал между обновлениями тикета, в мс
    requestInterval: 10 * 60000, // 10 min
    // параметры передаваемые в asker
    // указание host или url обязательно
    // https://github.com/nodules/asker
    asker: {
        // …
    },
    tvm: {
        // client_id TVM приложения
       id: 55,
        // Секрет для подписи ключа
        secret: 'secret'
    }
};
```

## Пример использования
```javascript
var TicketGetter = require('tvm-ticket-getter');
var config = {
    asker: {
        host: 'tvm-api-test.yandex.net',
        protocol: 'https:',
        port: 443
    },
    tvm: {
        id: 55,
        secret: 'secret'
    }
};
var getter = TicketGetter.createTicketGetter(config);
getter.on(
    'ticket',
    function (ticket) {
        console.log('ticket', ticket);
    }
);
getter.on(
    'error',
    function (error) {
        console.log('error', error);
    }
);
getter.start();

```
