r109473
#b-vcard-banners#

##Описание##
Блок списка баннеров для мастера визиток, управляющий списком баннеров.

Состоит из блока фильтрации и списка элементов баннеров, каждый из которых,
включает в себя обертку с рамочкой вокруг превью баннера и кнопками действий.

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[heliarian](https://staff.yandex-team.ru/heliarian)

###Где используется###
Используется в блоке `b-manage-vcards`

###Модели###

* `m-vcard` - модель визитки
* `m-banner` - модель баннера
* `m-filter-vcards-banners` - модель фильтра списка баннеров

##Roadmap & known issues##

* не передавать `consts`, а использовать константы из утилит

##Пример##

```

    {
        block: 'b-vcard-banners',
        consts: CONSTS,
        campaign: campaign, // объект кампании
        vcards: vcards, // список визиток
        banners: banners // список баннеров
    }
```
