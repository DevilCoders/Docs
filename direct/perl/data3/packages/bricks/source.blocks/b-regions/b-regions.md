#b-regions-tree#

##Описание##
Блок выбора регионов. Внутри себя содержит дерево регионов `b-regions-tree` и контролы для поиска и быстрого выбора.
Умеет отображать список ссылок быстрого выбора переданных в параметре `quickSelectRegions`, ссылку Мой регион, который передается
в параметре `quickSelectUserRegion`.

##Меинтейнеры##
[a-urukov](https://staff.yandex-team.ru/a-urukov)
[ngraf](https://staff.yandex-team.ru/ngraf)

##Пример##
```javascript
{
    block: 'b-regions',
    regions: [{ id: 100, name: "Россия", inner: [{ id: 101, name: "Москва" }] }],
    disableRegions: [1,2],
    quickSelectRegions: [
        { id: 1, name: iget('Москва и область') },
        { id: 10174, name: iget('Санкт-Петербург и область') },
        { id: 187, name: iget('Украина') },
        { id: [225, 166, 169], name: iget('Россия, СНГ и Грузия') }
    ],
    quickSelectUserRegion: {
       id: 1,
       name: "Россия"
    }
}
```
