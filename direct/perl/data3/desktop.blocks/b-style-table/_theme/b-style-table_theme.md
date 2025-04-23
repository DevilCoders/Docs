Тема bordered, кроме бордера добавляет для элементов row паддинги, а так же фон для шапки,
которая состоит из:
Шапки (elem: 'head'), в которой находятся строки с модификатором position_top и type_bottom
[
    {
        elem: 'row',
        elemMods: {
            position: 'top'
        }
    },
    {
        elem: 'row',
        elemMods: {
            position: 'bottom'
        }
    }
]
И опциональной строки, с модификатором type_bordered, которая может
находится в основной таблице, под шапкой, или же отсутствовать
{
    elem: 'row',
    elemMods: {
        type: 'bordered'
    }
}
