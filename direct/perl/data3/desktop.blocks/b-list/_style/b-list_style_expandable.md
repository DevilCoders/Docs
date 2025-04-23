Блок списка с модификатором, добавляющим функциональность раскрываемого/скрываемого списка b-list

Пример, блок с ограничением в 5 элементов списка и кнопками показать/скрыть:

{
    block: 'b-list',
    mods: { style: 'expandable' },
    content: [
        { elem: 'header', content: 'List title' },
        {
            elem: 'list',
            limit: 5,
            content: ['List item 1', 'List item 2', 'List item 3', 'List item 4'].map(function(item) {
                return { elem: 'item', content: item };
            })
        },
        { elem: 'expand', content: iget('показать все') },
        { elem: 'collapse', content: iget('скрыть') }
    ]
}


Элементы expand и collapse опциональны (если отсутствуют оба или есть только один из них, то недостающая поведенческая
функциональность компенсируется интерфейсными методами блока)
