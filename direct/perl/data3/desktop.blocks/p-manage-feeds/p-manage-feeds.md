#p-manage-feeds#

##Описание##
Страница с списком фидов.

Использует технологию [History API](https://github.com/bem/bem-history) для обновления интерфейса без перезагрузки страницы.
Состояние интерфейса фиксируется во view-модели блока `b-feeds-list`, по которой строится его содержимое.  

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[eemelin](https://staff.yandex-team.ru/eemelin)

###Взаимодействие с другими блоками###
Содержит в себе блок `b-feeds-list`, который умеет обновлять своё содержимое при изменении его view-модели.
    
###Модели###    

* `dm-feed-list` - модель с данными списка фидов
* `b-feeds-list.vm` - view-модель списка фидов
