#b-stat-phrases-manager

##Описание
Блок строит сгруппированные по кампаниям списки фраз. 
Предоставляет возможность редактировать фразы и выставить ставки перед добавлением в группу.
![preview](https://jing.yandex-team.ru/files/skywhale/2017-01-24%2017-27-59.png)

###Автор
[skywhale](https://staff.yandex-team.ru/skywhale)

###Где используется
На табах «Поисковые запросы» и «Дополнительные фразы» статистики.

###Модификаторы
- `type`
    - `mol` - напротив группы фраз будут ссылки на кампанию
    - `moc` - напротив группы фраз не будет ссылок на кампанию

###Взаимодействие с другими блоками
- `b-stat-table-phrases-popup` - попап обертка над `b-stat-phrases-manager`
- `b-edit-phrase-price` - инпуты для ввода, валидации ставки на поиске или в сетях
- `b-edit-phrase-price-stat-popup` - попап для одновременного ввода, валидации ставки на поиске и в сетях. Также используется для выставления «Единой цены».
- `b-phrases-auction-popup` - попап с торгами(«Цена клика ключевой фразы»)
 
##Пример
```
{
    block: 'b-stat-phrases-manager',
    mods: { 'stat-type': 'mol' },
    js: {
        // информация о кампаниях(стратегия, тип)
        campaigns: {
            c1: { type: 'text', strategy: /* примеры стратегий можно найти в тестах */ },
            c2: { type: 'text', strategy: /* примеры стратегий можно найти в тестах */ },
            c3: { type: 'text', strategy: /* примеры стратегий можно найти в тестах */ }
        },
        // информация о группах
        groups: {
            g1: { groupName: 'Группа 1', adgroupId: 'g1', campName: 'Кампания 1', cid: 'c1' },
            g2: { groupName: 'Группа 2', adgroupId: 'g2', campName: 'Кампания 1', cid: 'c1' },
            g3: { groupName: 'Группа 3', adgroupId: 'g3', campName: 'Кампания 2', cid: 'c2' },
            g4: { groupName: 'Группа 4', adgroupId: 'g4', campName: 'Кампания 3', cid: 'c3' }
        },
        // список фраз
        phrases: [
            { pid: 'g1', src_phrase: 'Фраза 1', src_type: 'ext_phrase' },
            { pid: 'g2', src_phrase: 'Фраза 2', src_type: 'ext_phrase' }
        ],
        // валюта
        currency: 'RUB'
    }
}
```
