#b-shared-popup#

##Описание##
Попап инстанс которого могут использовать разные блоки на одной странице. 

Блоки могут обновлять содержимое попапа при этом сам попап пересоздаваться не будет.

Созданный инстанс является декоратором над попапом и предоставляет проксирующий интерфейс на методы:

* `hide`
* `show`
* `toggle`
* `isShown`
* `setContent`
* `repaint`

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[belyanskii](https://staff.yandex-team.ru/belyanskii)

##Пример##

```

    // создание экземпляра попапа с нужными настройками
    var popup = BEM.blocks['b-shared-popup'].getInstance(
        { animate: 'yes' }, 
        { directions: ['right-middle-middle', 'top-left-right'] });
    
    // и использование его далее с любым контентом и хозяином хвоста 
    popup
        .setContent(BEMHTML.apply({ block: 'content-block' }))
        .toggle(this.elem('link'));
        
    // можно менять и содержимое 
    popup.setContent(BEMHTML.apply({ block: 'content-block2' }));
    
    // ... и хозяина
    popup.toggle(this.elem('link2'));
```
