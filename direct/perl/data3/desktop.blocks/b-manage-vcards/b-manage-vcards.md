r102707
#b-manage-vcards#

##Описание##
Блок управления мастером визиток.

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[heliarian](https://staff.yandex-team.ru/heliarian)

###Где используется###
Используется как основной блок page-блока `p-manage-vcards`.
   
###Взаимодействие с другими блоками###
Создает и контролирует процесс общения между списками баннеров `b-vcard-banners` и визиток `b-vcards`, назначением и отвязкой визиток.
    
###Модели###    

* `m-vcard` - модель визитки
* `m-banner` - модель баннера

##Roadmap & known issues##

* не передавать `consts`, а использовать константы из утилит
* не передавать `ulogin`, а использовать константы из утилит

##Пример##

```

    {
        block: 'b-manage-vcards',
        consts: CONSTS,
        campaign: campaign, // объект кампании
        vcards: vcards, // список визиток
        banners: banners, // список баннеров
        ulogin: userLogin // логин пользователя 
    }
```
