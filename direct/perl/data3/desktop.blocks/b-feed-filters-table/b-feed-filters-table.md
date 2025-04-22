#b-feed-filters-table#

##Описание##
Блок списка группированных фильтров для фидов в динамических группах и смарт-баннерах

###Автор###
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[heliarian](https://staff.yandex-team.ru/heliarian)

###Где используется###
Используется в блоке `b-campaign-group` в элементе `phrases` на модификаторе `_type_performance`

###Взаимодействие с другими блоками###
На макроуровне взаимодействует через DM с блоком `b-prices-constructor` в `b-online-set-phrases-prices`

##Особенности##
Основан на блоке `b-dynamic-conditions-table`

##Пример##

```

    {
        block: 'b-feed-filters-table',
        mods: {
            loading: 'yes',
            platform: 'default',
            strategy: ({
                autobudget_avg_cpc_per_camp: 'avg-cpc',
                autobudget_avg_cpc_per_filter: 'avg-cpc',
                autobudget_avg_cpa_per_camp: 'avg-cpa',
                autobudget_avg_cpa_per_filter: 'avg-cpa'
            })[campaignStrategyNetName] || 'default' // где campaignStrategyNetName - имя net стратегии
        },
        group: {}, // объект группы
        nowOptimizingBy: netNowOptimizingBy, // где netNowOptimizingBy - опциональный тип оптимизации со значениями 'CPC'|'CPA'
        currency: campaignCurrency, // где campaignCurrency - валюта для кампании
        showStat: true // true|false
    }
```
