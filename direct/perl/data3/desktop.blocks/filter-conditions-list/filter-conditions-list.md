#filter-conditions-list#

##Описание##
Список условий в фильтре для фида

###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

###Где используется###
Родительский блок - filter-edit
Применяется для смарт-баннеров, в будущем - для диначиеских баннеров

###Взаимодействие с другими блоками###
Для работы с элементами списка использует composite
Для подписки на события - i-subscription-manager
Блок отдельного условия в списке - filter-condition-edit

##Пример##

`
    {
        block: 'filter-conditions-list',
        conditions: [{ field: 'categoryId', relation: '<', value: '3' }]
    }

`
