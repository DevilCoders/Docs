#tabs-menu_with-confirm_yes#

##Описание##
Меню табов, запрашивающее подтвержление при активации таба.
Отправляет событие ask-confirm с данными
{
    prevIndex: this.indexOfTab(prev),
    current: elem,
    prev: prev,
    currentIndex: this.indexOfTab(elem),
    deferred: deferred
}

Активация таба происходит только при deferred.resolve();

###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

