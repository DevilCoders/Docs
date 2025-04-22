r103622
#b-vcards#

##Описание##
Блок списка визиток для использования в мастере визиток.

Состоит из блока фильтрации, списка элементов визиток, блока для iframe редактирования/просмотра визитки.

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[heliarian](https://staff.yandex-team.ru/heliarian)

###Где используется###
Используется в блоке `b-manage-vcards`

###Модели###

* `m-vcard` - модель визитки
* `m-banner` - модель баннера
* `m-filter-vcards` - модель фильтра списка визиток

##Roadmap & known issues##

* не передавать `ulogin`, а использовать константы из утилит

##Пример##

```

    {
        block: 'b-vcards',
        campaign: campaign, // объект кампании
        vcards: vcards, // список визиток
        ulogin: userLogin // логин пользователя
    }
```
