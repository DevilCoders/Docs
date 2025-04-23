#b-feed-filters-group#

##Описание##
Блок-контейнер, содержащий в себе:

 - блок группового изменения ставки на группе фильтров
 - блок фильтра с его контролами управления ставкой на фильтре
 - тоглер скрытия/показа отключенных фильтров

###Автор###
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[eemelin](https://staff.yandex-team.ru/eemelin)

###Где используется###
Используется в блоке `b-feed-filters-table` как основное содержимое

###Взаимодействие с другими блоками###
Блок `live`'овый и просыпается от инициализации внутренних блоков `b-feed-filter` и `b-edit-phrase-price`, а
также при обращении из блока `b-groups-list`

###Модели###
Список VM:

 - `vm-sync-dm` базовая модель для VM блока

Список DM:

 - `dm-dynamic-media-group` дата модель

##Особенности##
Основан на блоке `b-dynamic-conditions-group`
Реализует интерфейс `i-sortable-interface`

##Пример##

```

    {
        block: 'b-feed-filters-group',
        mods: {
            state: 'active', // 'active'|'suspended'
            strategy: 'avg-cpa' // 'default'|'avg-cpa'|'avg-cpc'|'net'|'search'|'different-places'
        },
        group: {}, // объект группы
        nowOptimizingBy: 'CPA', // опциональное со значениями 'CPC'|'CPA'
        showStat: true // true|false
    }
```
