# xiva-websocket
Модуль для работы с сервисом уведомлений [Xiva](https://console.push.yandex-team.ru/#api-reference-websocket).

## Install

```bash
npm install --save @yandex-int/xiva-websocket
```

## Usage
```js
var xiva = new window.Ya.XIVA({
    api: 'custom API URL', 
    reconnectMaxTimeout: XXX, 
    reconnectCooldown: YYY,
    reconnectTimeoutIncrement: ZZZ
    urlParams: {
        ... 
    }
})

xiva.addEventListener('open', function() {...});
xiva.addEventListener('message', function() {...});
xiva.addEventListener('close', function() {...});
xiva.addEventListener('error', function() {...});
```

####Дополнительные параметры
Передаются объектом new window.Ya.XIVA({...});

##### urlParams 
по-умолчанию - ничего нет  
Параметры из доки [api-reference-websocket](https://console.push.yandex-team.ru/#api-reference-websocket)

##### api 
по-умолчанию - `wss://push.yandex.ru/v2/subscribe/websocket`  
Урл для доступа к ручке, если нужно будет использовать тестовую ручку например


##### reconnectMaxTimeout 
по-умолчанию - 2000ms  
В рамках этого значения будет выбран первый интервал переплдключения в случае разрыва  


##### reconnectCooldown 
по-умолчанию - 10000ms    
Через это время после успешного подключения будет сброшен таймаут переподлючения, который набрался за прошлые обрывы


##### reconnectTimeoutIncrement 
по-умолчанию - 500ms  
Число на которое будет увеличиваться таймер переподлючения

При базовых значениях:  
1. Допустим был разрыв
2. Случайно выбирается значение от 0 до 2000, допустим 750ms (reconnectMaxTimeout)  
3. Через 750ms будет вторая попытка подключения
4. Если она провалится, то будет добавлено ещё 500ms (reconnectTimeoutIncrement)
5. Если через 1250ms будет успешное подключение, модуль подождёт 10000ms и выполнит пунтк 1

## Unit tests
```bash
sh tests/run
```

Запускает PhantomJS для проверки автотестами
