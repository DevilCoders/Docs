#i-event-bus#

##Описание##
Шина событий.

Служит прослойкой при необходимости работы с событиями, например, при инициировании их во фрэймах (см. `b-iframe`) или 
нативных попапах (см. `b-modal-popup-opener`).

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[belyanskii](https://staff.yandex-team.ru/belyanskii)

##Roadmap & known issues##
Известные проблемы и планы по развитию блока

##Пример##

Подписываемся на события в шине на хост-странице:

```

    BEM.blocks['i-event-bus']
        // создание шины с именем будущего окна
        .getEventBus('[unique event bus name]')
        .on('hello', function(e, data) { 
            alert(data); 
        });
```

Затем на хост-странице либо открываем нативный попап `window.open('http://some.host', '[unique event bus name]');`

либо iframe любым удобным способом `<iframe src='http://some.host' name='[unique event bus name]'>`

с именем, совпадающим с названием шины.

В открываемом документе триггерим событие:

```

    BEM.blocks['i-event-bus']
        .getEventBus(window.name)
        .trigger('hello', 'dude');
``` 

Работает в обе стороны, прозрачно для обеих сторон. То есть если требуется идентифицировать источник события, то
это необходимо сделать самому (например, назвать должным образом события)

Не работает кроссдоменно по понятным причинам.
