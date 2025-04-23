#b-dropdown-trigger#

##Описание##
По нажатию на кнопку показывает попап и переданный список, по нажатию на элемент списка
закрывает попап и генерирует событие (по-умолчанию click но можно переопределить)

###Автор### 
[grimfrid](https://staff.yandex-team.ru/grimfrid )

###Где используется###
`b-charts-manager`
   
###Взаимодействие с другими блоками###
Использует `dropdown2` и `b-chooser`

##Roadmap & known issues##
Известные проблемы и планы по развитию блока

##Пример##

```
    {
        block: 'b-dropdown-trigger',
        button: 'Экспорт',
        js: {
            eventName: 'export'
        },
        items: [
            { content: 'PNG', name: 'png' },
            { content: 'JPEG', name: 'jpeg' },
            { content: 'SVG', name: 'svg' },
            { type: 'separator' },
            { content: iget('Напечатать'), name: 'print' }
        ]
    }

```
