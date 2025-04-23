#list-style#

##Описание##
Блок для применения стилей списка сторонним блоком.
Под модификаторами размещаются возможные настройки.

theme - внешний вид
numeration - альтернативный вариант list-style: decimal inside

###Автор###
[eemelin ](https://staff.yandex-team.ru/eemelin )


##Как пользоваться и расширять##
Блок расширяется новыми темами, новыми настройками не связанными с внешним видом (например, кастомная маркировка списка или рамка вокруг элементов )

##Пример##

Применяется на блоке и его элементах через миксы:

`
    block: 'some',
    mix: { block: 'list-style', mods: { theme: 'zebra' } },
    content: {
        elem: 'items-wrap',
        mix: { block: 'list-style', elem: 'items' },
        content: someData.map(function(data) {
            return {
                block: 'some',
                elem: 'child-elem',
                mix: { block: 'list-style', elem: 'item' },
                data: item
            }
        })
    }
`
