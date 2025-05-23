# autoinsert

Блок на текущий момент релизован только под модификатором `view_table-row`.

Структура:
```styl
.autoinsert // Блок автоподставы
    __option // Первый кликабельный элемент для установки __value
    __option // Второй кликабельный элемент для установки __value
    //...
    __value // Текущее значение с инпутами и чекбоксами, которое будет отправлено при сабмите
```

```javascript
{
    block: 'autoinsert',
    cellCount: 4, // Количество колонок в таблице
    mods: {
        view: 'table-row'
    },
    aiDisable: true, // Не отображать автоподставу на добавление после удаления
    value: {
        // Bemjson отрендеренной автоподставы (С инпутами, селектами). Массив длиной равной cellCount
        cells: cells(value),
        // Bemjson в виде кликабельного элемента автоподставы, по клику в который рендерится cells
        aiDisplay: aiDisplay(value)
    },
    // mix к элементу __value.
    valueMix: { block, elem: 'table-row', elemMods: { 'is-empty': true } },
    // Добавить к текущему отображаемому элементу автоподставу на удаление
    aiDelete: true,
    autoinserts: [ // Массив с автоподставами
        {
            // Тип автоподставы
            type: 'add', // 'add' | 'replace'
            value: {
                // Bemjson отрендеренной автоподставы (С инпутами, селектами). Массив длиной равной cellCount
                cells: [1, 2, 3, 4],
                // Bemjson в виде кликабельного элемента автоподставы, по клику в который рендерится cells
                aiDisplay: [1, 2, 3, 4]
            }
        }
    ]
}
```
