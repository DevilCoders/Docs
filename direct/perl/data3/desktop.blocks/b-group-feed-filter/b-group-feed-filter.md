#b-group-feed-filter#

##Описание##
Блок-контейнер, содержащий в себе блок фильтра и контролы управления ставкой на фильтре

###Автор###
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[eemelin](https://staff.yandex-team.ru/eemelin)

###Где используется###
Используется в блоке `b-feed-filters-group` как основное содержимое

###Взаимодействие с другими блоками###
`live` блок, "просыпается" от инициализации внутренних блоков `b-feed-filter` и `b-edit-phrase-price`

###Модели###
Список VM:

 - `vm-feed-filter` базовая модель для VM блока

Список DM:

 - `dm-dynamic-media-group` или `dm-dynamic-group` дата модель-контейнер (содержит в себе DM для VM)
 - `dm-feed-filter` дата модель

##Особенности##
Основан на блоке `b-group-dynamic-condition`

##Пример##

```

    {
        block: 'b-group-feed-filter',
        mods: {
            first: 'yes', // 'yes' или не задан
            strategy: 'avg-cpa'
        },
        group: {}, // объект группы
        filter: {}, // объект фильтра
        showStat: true // true|false
    }
```
