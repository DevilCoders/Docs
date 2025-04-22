#b-chart-filters

##Описание
Блок для управления фильтрами графика, фильтры помещаются в content блока,
к каждому фильтру должен быть примиксован, элемент название которого соответствует названию фильтра,
используется в дальнейшем для получения фильтра по имени `block.getFilter(name)`
Например:
```
{
    block: 'b-chart-filters',
    elem: 'view'
}
```

###Автор 
[grimfrid](https://staff.yandex-team.ru/grimfrid )

###Где используется
В `b-charts-manager`
   
###Взаимодействие с другими блоками
Взаимодействует с блоком `b-chart-filter-control`

## Модфикаторы

**limits** - описывает логику взаимодействия конкретных фильтров между собой

##Roadmap & known issues
-

##Пример

```
    {
        block: 'b-chart-filters',
        mods: {
            limits: 'columns-groups'
        },
        content: [
            {
                block: 'b-chart-filter-control',
                mods: { type: 'select' },
                mix: [
                    {
                        block: 'b-chart-filters',
                        elem: 'filter'
                    },
                    {
                        block: 'b-chart-filters',
                        elem: 'columns'
                    }
                ],
                name: 'columns',

                control: {
                    mods: {
                        multi: 'yes',
                        'group-limit': 2
                    },
                    values: [
                        { text: 'Показы', value: 'shows', group: 'group1' },
                        { text: 'Клики', value: 'clicks', group: 'group1' },
                        { text: 'CTR, %', value: 'ctr', group: 'group2' },
                        { text: 'Цена, руб', value: 'price', group: 'group3' }
                    ]
                }
            },
            {
                block: 'b-chart-filter-control',
                mods: { type: 'select' },
                mix: [
                    {
                        block: 'b-chart-filters',
                        elem: 'filter'
                    },
                    {
                        block: 'b-chart-filters',
                        elem: 'groupBy'
                    }
                ],
                name: 'groupBy',

                control: {
                    text: iget('Срез'),
                    values: [
                        { text: 'Пол', value: 'gender' },
                        { text: 'Возраст', value: 'age' }
                    ],
                    messages: {
                        switcher: {
                            disabled: iget('Для отображения среза оставьте 1 столбец')
                        }
                    }
                }

            }
        ]
    }
```
