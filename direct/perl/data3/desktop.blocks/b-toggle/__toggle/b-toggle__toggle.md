Элемент toggle - контейнер для панелей. Сами панели - это элементы item. Контент для элемента toggle можно тоже описать в развернутом виде. Для этого нужно вместо поля items использовать поле content:

{
    elem: 'toggle',
    content: [
        {
            elem: 'item',
            elemMods: { state: 'hidden' },
            content: 'panel1'
        },
        {
            elem: 'item',
            elemMods: { state: 'visible' },
            content: 'panel2'
        }
    ]
}
