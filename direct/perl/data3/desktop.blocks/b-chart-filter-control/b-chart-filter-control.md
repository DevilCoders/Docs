#b-chart-filter#

##Описание##
Блок обертка для контролов, позволяется использовать контролы как фильтры
в `b-chart-filters`

###Автор### 
[grimfrid](https://staff.yandex-team.ru/grimfrid )

###Где используется###
`b-chart-filters`
   
###Взаимодействие с другими блоками###
На данный момент в зависимости от модификатора взаимодействует с:
`b-select-filter`,
`radio-button`

##Как пользоваться и расширять##
Добавляем модификатор, описываем API (скелет методов в базовом .js)

##Пример##

```
{
    block: 'b-chart-filter-control',
    mods: { type: 'select' },
    mix: { block: 'b-chart-filters', elem: 'filter' },
    name: 'columns',

    control: {
        mods: {
            multi: 'yes',
            'group-limit': 2
        },
        text: iget('Столбец'),
        values: this.ctx.columns,
    
        messages: {
            'filter-item': {
                'group-limit': iget('Нельзя одновременно показать данные 3-х типов столбцов. Отключите часть параметров')
            }
        }
    }
}

```
