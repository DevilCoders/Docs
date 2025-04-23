#b-select-filter

##Описание
Блок для выбора значения фильтра, умеет выбирать как и один вариант, так и несколько,
умеет в выключение выриантов, в зависимости от выбора других (если они разделены по группам)

###Автор
[grimfrid](https://staff.yandex-team.ru/grimfrid )

###Где используется
Еще не используется
   
###Взаимодействие с другими блоками
Использует `dropdown2` и `b-chooser`
  
##Как пользоваться и расширять
С удовольствием

##Входные данные
- {String} `[text]` - название фильтра (показывается в кнопке)
- {Array<{text, value, [group], [selected], [disabled]}>} `options` - массив вариантов
- {Object} `[messages]` - объект содержащий предупреждающие сообщения

## Модификаторы 

###multi
Включает режим множественного выбора (multi: 'yes')

###disabled
Выключает контрол и если передан текст в `messages.switcher.disabled` то при
наведении на контрол отобразит его

###group-limit
Есть смысл использовать только вместе с `multi_yes`
Устанавливает лимит групп, варианты из которых можно выбрать одновременно.
Например, мы передаем несколько вариантов, которые разбиты по группам (поле group):
- если group-limit = 1, то выбрав вариант из первой группы, варианты из остальных групп
перейдут в состояние disabled
- если group-limit = 2, то выбрав варианты из первой и третьей групп, варианты из остальных групп
перейдут в состояние disabled

Если передан текст в `messages.filter-item.group-limit`, но при наведении
на выключенный вариант, отобразиться сообщение

**Внимание**: при использовании этого модификатора, в каждом объекте внутри
`options` должно быть поле group

##Roadmap & known issues
-

##Примеры

Простой пример, работает как обычный dropdown, в кнопке будет отображено: `Filter Name: не выбран`,
если будет выбран какой-нибудь вариант то: `Filter Name: {option.text}` 
```
{
    block: 'b-select-filter',
    text: 'Filter Name',
    options: [
        { text: 'testName', value: 'testValue' },
        { text: 'testName 1', value: 'testValue1' },
        { text: 'testName 2', value: 'testValue2' },
        { text: 'testName 3', value: 'testValue3' }
    ],
}

```

Фильтр в режиме мультивыбора, по-умолчанию элементы `testName` и `testName 1` будут выбраны, вариант `testName 3`
будет недоступен для выбора.
```
{
    block: 'b-select-filter',
    mods: {
        multi: 'yes'
    },
    text: 'Filter Multi',
    options: [
        { text: 'testName', value: 'testValue', selected: 'yes' },
        { text: 'testName 1', value: 'testValue1', selected: 'yes' },
        { text: 'testName 2', value: 'testValue2' },
        { text: 'testName 3', value: 'testValue3', disabled: 'yes' }
    ],
    messages: {
        switcher: {
            disabled: 'Для использования фильтра, сделайте что-то хорошее'
        }
    }
}
```

Аналогично предыдущему варианту, но контрол будет выключен, и при наведении будет появляться tooltip с сообщением
```
{
    block: 'b-select-filter',
    mods: {
        multi: 'yes',
        disabled: 'yes'
    },
    text: 'Filter Multi',
    options: [
        { text: 'testName', value: 'testValue', selected: 'yes' },
        { text: 'testName 1', value: 'testValue1', selected: 'yes' },
        { text: 'testName 2', value: 'testValue2' },
        { text: 'testName 3', value: 'testValue3', disabled: 'yes' }
    ],
    messages: {
        switcher: {
            disabled: 'Для использования фильтра, сделайте что-то хорошее'
        }
    }
}
```

Пример с лимитом групп, по умолчанию выбрано 2 элемента из разных групп (1 и 3), варианты `testName 1` и `testName 3`
будут в режиме disabled, `testName 2` будет доступен для выбора. Если пользователь оставит выбранными варианты только
из одной группы, то остальные будут доступны.
```
{
    block: 'b-select-filter',
    mods: {
        multi: 'yes',
        'group-limit': 2
    },
    text: 'Filter Name',
    options: [
        { text: 'testName', value: 'testValue', group: 'group1', selected: 'yes' },
        { text: 'testName 1', value: 'testValue1', group: 'group2' },
        { text: 'testName 2', value: 'testValue2', group: 'group1' },
        { text: 'testName 3', value: 'testValue3', group: 'group2' },
        { text: 'testName 4', value: 'testValue4', group: 'group3', selected: 'yes' }
    ],
    messages: {
        switcher: {
            disabled: 'Для отображения среза оставьте 1 столбец'
        },
        'filter-item': {
            'group-limit': 'Нельзя одновременно показать данные 3-х типов столбцов. Отключите часть параметров'
        }
    }
}
```
