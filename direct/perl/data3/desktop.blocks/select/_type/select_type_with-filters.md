Блок селекта с произвольным блоком фильтрации

Пример:

{
    block: 'select',
    mods: { size: 'xs', theme: 'normal', type: 'with-filters' },
    content: [
        {
            elem: 'filters',
            filter: {
                block: 'block-filter-which-implements-i-handle-filter'
            },
            empty: {
                block: 'block-with-notice-that-nothing-to-show'
            }
        },
        {
            elem: 'control',
            content: ['item 1', 'item 2', 'item 3', 'item 4'].map(function(client) {
                return {
                    elem: 'option',
                    attrs: { value: client },
                    content: client
                };
            })
        }
    ]
}

Условный блок block-filter-which-implements-i-handle-filter должен реализовывать интерфейс i-handle-filter

Блок block-with-notice-that-nothing-to-show может быть добавлен опционально, он будет показан, если в
результате фильтрации не будет найден ни один удовлетворяющий элемент.

При фильтрации методу filter блока фильтра передается значение value DOM элемент option, проанализировав который, метод
должен вернуть true или false, в зависимости от того, надо показать или спрятать элемент соответственно.

За набор фильтров и их поведение отвечает сам блок фильтра.
