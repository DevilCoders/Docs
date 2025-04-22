#Контрол выбора набора элементов из списка

##Мейнтейнеры 
@a-urukov

По умолчанию, истоничком данных для саджеста является блок i-multiselect-static-provider
Пример использования:
{
    block: 'b-badges-multiselect',
    mods: { type: 'campaigns' },
    items: campaigns,
    value: selected,
    hint: iget('Выберите кампании из списка'),
    content: [
        { elem: 'clear' },
        { elem: 'control' }
    ]
}
