#i-bem__interface#

##Описание##
Набор набор методов добавленных в прототип BEM.DOM для работы с интерфейсами,
которые имплементируют классы блоков. Позволяет искать внутри инстанса блока или на нем самом блоки
с определенными интерфейсами.

###Меинтейнеры###
[ngraf](https://staff.yandex-team.ru/ngraf)

##Пример##
```javascript
BEM.DOM.decl('my-block', [

    getBlockWithInterface() {
        return this.findBlockByInterfaceInside('custom-interface');
    }

]);
```

