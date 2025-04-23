#i-modal-popup-inner-block-interface#

##Описание##
Интерфейс для блока, встраиваемого внутрь b-modal-popup-decorator.

###Меинтейнеры###
[ngraf](https://staff.yandex-team.ru/ngraf)

##Пример##
```javascript
BEM.DOM.decl({ block: 'b-block-popup-content', implements: 'i-modal-popup-inner-block-interface' }, {

    /**
     * Были ли изменения
     * @returns {$.Deferred<Boolean>}
     */
    isChanged: function() {
        var deferred = $.Deferred();

        deferred.resolve(!u._.isEmpty(this.findBlockInside('input').val()));

        return deferred;
    }

});
```
