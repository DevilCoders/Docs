#b-href-popup#

##Описание##
Попап ввода ссылки.

###Автор### 
[dima117a](https://staff.yandex-team.ru/dima117a )

###Где используется###
- b-image-add-loader

##Пример##

```
    // создаем попап, в качестве параметров передаем callback и контекст вызова для него 
    var popup = BEM.DOM.blocks['b-href-popup'].create(function(href) {
        ...
    }, this);
    
    popup.show();

```
