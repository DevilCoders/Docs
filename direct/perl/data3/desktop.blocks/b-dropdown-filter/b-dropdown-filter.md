r103622
Блок для фильтрации в виде выпадающего попапа.

Управляется через модель (с 1 обязательным полем value), которая явно задаётся через i-glue.

Должен принимать в контекст items массив с { value, text } объектами значения фильтра и текста его метки.
Может принимать в контексте popup настройки mods и js для elem popup блока dropdown.
Может принимать в контексте footer bemjson "подвала" попапа фильтра (для возможности накидать произвольного контента).

Пример:

{
    block: 'b-dropdown-filter',
    js: {
        modelName: 'm-filter-for-dropdown',
        modelData: { value: 'all' }
    },
    popup: {
        js: { directions: 'bottom-left' },
        mods: { adaptive: 'no', animate: 'no' }
    },
    items: [
        { value: 'all', text: iget('все') },
        { value: 'half', text: iget('половина') },
        { value: 'empty', text: iget('ничего') }
    ],
    footer: [
        'Спасибо академии, маме и моему школьному учителю'
    ]
}
