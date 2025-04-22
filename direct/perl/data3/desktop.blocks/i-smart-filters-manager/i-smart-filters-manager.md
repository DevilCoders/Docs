#i-smart-filters-manager#

##Описание##
Блок для работы с условиями фильтрации типа:
 - filter - доступны фильтры A, B, C
 - для filter = A доступны subFilter a, b и c
 - для filter = B доступны subFilte a, b, e, d

Если выбран filter = A и subFilter = a, то второй раз filter = A и subFilter = a выбрать нельзя
Если для filter = A уже выбраны subFilter a, b и c
statesMap - карта имеющихся фильтров и саб-фильтров  **constraints пока не реализованы**:

    {
        //порядок фильтров
        orderedFiltersNames: ['filter1', 'filter2', 'filter3']
        filter1: {
            orderedSubFiltersNames: ['subFilter1', 'subFilter2', 'subFilter3'],
            subFilters: {
                subFilter1: {
                    //не может быть выбран, если выбран 'subFilter3'
                    constraints: ['subFilter3']
                }
            },
            //не может быть выбран, если выбран filter3
            constraints: ['filter3']
        }

    }





###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

###Где используется###
filter-conditions-list


##Пример##

`
    BEM.create('i-smart-state-manager', { statesMap: statesMap });

`
