r103821
# Блок выбора кампании.

##Мейнтейнеры 
@dima117a

Представляет собой блок выпадающего списка select с опциональной фильтрацией по кампаниям.

На вход принимает:
 - name имя DOM элемента блока select
 - mods хэш модификаторов для блока select
 - mix хэш модификаторов для блока select
 - inputHint блок хинта поля ввода для блока фильтрации
 - emptyHint блок сообщения при пустом результате поиска
 - campaigns список объектов кампаний, имеющий поля:
   - cid идентификатор кампании (обязательно)
   - name название кампании (обязательно)
   - selected флаг выбранного элемента выпадающего списка (опционально)

Пример:

```javascript
{
    block: 'b-campaigns-select',
    mods: {
        disabled: 'yes',
    },
    mix: { block: 'b-my-new-block', elem: 'campaigns-select' },
    inputHint: [
        {
            block: 'b-icon',
            mods: { 'size-13': 'find' }
        },
        '&nbsp;',
        iget('Найти кампанию по номеру или названию')
    ],
    emptyHint: iget('Нет кампаний, соответствующих фильтру'),
    name: 'cid',
    campaigns: [{ cid: 1, name: 'campaign 1' }, { cid: 2, name: 'campaign 2', selected: true }]
}
```
