//r102680
#b-iframe#

##Описание##
Блок для iframe.

В основном смысл блока в том, чтобы в runtime создавать и управлять iframe средствами bemhtml, а не через jQuery.

Страница загружаемая с помощью этого блока имеет возможность передавать сообщения через шину событий (см. `i-event-bus.md`).

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[belyanskii](https://staff.yandex-team.ru/belyanskii)

##Пример##

BEMHTML:

```

    {
        block: 'b-iframe',
        mods: { hidden: 'yes' }
        src: '/path/to/dest'
    }
```

JS:

```

    var block = ...,
        bus = block.getEventBus(); // шина событий для получения сообщений из iframe
```

Для более живого примера см. блок `p-edit-vcard-headless`.
