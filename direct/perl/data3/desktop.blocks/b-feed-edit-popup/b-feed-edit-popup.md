#b-feed-edit-popup#

##Описание##
Попап редактирования фидов.

Умеет сохранять редактируемный или новый фид и оповещать об этом через событие `save`, при отмене 
редактирования триггерит событие `cancel`.

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[eemelin](https://staff.yandex-team.ru/eemelin)

###Где используется###
Используется для редактирования и создания фидов в блоке `b-feeds-list`
    
###Модели###    

* `b-feed-edit-popup.vm`
* `dm-feed`
* `vm-feed`

##Пример##

###Редактирование фида###

```

    {
        block: 'b-feed-edit-popup',
        feed: BEM.MODEL.getOne('vm-feed').toJSON()
    }
```

###Создание фида по умолчанию###

```

    {
        block: 'b-feed-edit-popup'
    }
```

###Создание фида с указанием источника фида###

```

    {
        block: 'b-feed-edit-popup',
        feed: {
            source: 'file'
        }
    }
```
