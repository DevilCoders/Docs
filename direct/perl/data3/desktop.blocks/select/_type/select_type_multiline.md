Блок многострочного селекта (<select size="5" />). По умолчанию размер равен 5, можно менять его передавая значение в контексте.

Важно! Передавать блок { block: 'button' } в content селекта не обязательно.

Пример:

{
    block: 'select',
    mods: { size: 'xs', theme: 'normal', type: 'multiline' },
    size: 10,
    content: {
        elem: 'control',
        content: ['item 1', 'item 2', 'item 3', 'item 4'].map(function(client) {
            return {
                elem: 'option',
                attrs: { value: client },
                content: client
            };
        })
    }
}
