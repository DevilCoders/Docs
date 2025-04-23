#i-infoblock#

##Описание##

Базовый блок инфоблока. Отвечает за обмен данными между клиентом и сервером.

Умеет отправлять POST-запросы с очередью сообщений.

Сервер, получая такое POST сообщение должен уметь:
 - извлекать JSON из тела сообщения
 - обрабатывать свойство queue от полученного JSON объекта
 - отправлять в качестве ответа список объектов, имеющих один из указанных представлений:
    - { uniqId: 'received from client unique id ', error: 'error message' }
    - { uniqId: 'received from client unique id ', response: 'service response' }

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[a-urukov](https://staff.yandex-team.ru/a-urukov)

###Где используется###

* `b-infoblock`

##Roadmap & known issues##

Подробнее о рефакторинге инфоблока см. в `b-infoblock.md`

* нужно перенести как транспортный код в `b-infoblock.utils.js`

##Пример##

```

    var messenger = BEM
        .create('i-infoblock', {
            url: '/infoblock/process_message',
            data: { uid: 'some uid', const_param: 'some not valuable param' }
        }),
        promise1 = messenger.sendEventMessage('update-last-opened'),
        promise2 = messenger.sendEventMessage('update-news-state', { ext_news_id: 'd-2014-05-28', ... });
        
    // через 1 мс уходит запрос
    // обработка ответа на сообщение 'update-last-opened'
    promise1
        .then(function(data) {})
        .fail(function(err) {});
     
    // обработка ответа на сообщение 'update-news-state'
    promise2
        .then(function(data) {})
        .fail(function(err) {});
     
    // хэндлеры resolve или reject для каждого из промисов будут вызваны в порядке создания промисов
```

###Пример ответа от сервера:###

```

    [
        {
            "uniqId": "uniq328", // значение uniqId приходит от клиента на сервер и просто отправляется обратно
            "response": {
                // какой ответ на 'update-last-opened'
            }
        },
        {
            "uniqId": "uniq330",
            "response": {
                // какой ответ на 'update-news-state'
            }
        }
    ]
```

Сообщения отправляются на сервер в том же порядке, в котором они были добавлены в очередь.
