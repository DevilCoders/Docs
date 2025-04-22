#b-help-link#

##NB! Не надо вручную настраивать положение иконки внутри (b-icon) и ставить vertical-align: top самому блоку!
Фокус разъедется!#

##Описание##
Блок для вывода ссылки помощи.

Является проксирующим блоком с целью настройки блока `b-modal-popup-opener` (см. `b-modal-popup-opener.md`)

Есть варианты отображения блока как только текста, только иконки, текст + иконка, положение иконки до/после текста.

###Автор###
[belyanskii](https://staff.yandex-team.ru/belyanskii)

###Модификаторы###

* `type: 'modal'` - включает красивый попап, по умолчанию не задан (режим нативного попап-окна)
* `icon: ['left', 'right']` - положение иконки относительно текста (если он есть), по умолчанию 'right'
* `align: ['middle', 'baseline', 'top']` - верт. выравнивание иконки, по умолчанию 'baseline'
* `margin: 'no'` - выключает отступ слева у блока, по умолчанию не задан (есть отступ)
* `decoration: ['no', 'yes']` - выключает подчеркивание текста (текст псевдоссылки декорирован), по умолчанию 'yes'

##Пример##

###Блок по умолчанию (без текста, иконка (?)):###
```

    {
        block: 'b-help-link',
        mods: { type: 'modal' },
        width: 710,
        height: 620,
        stretched: true,
        url: u.getHelpUrl('remote-trading')
    }
```

###Блок в виде текстовой псевдоссылки:###
```

    {
        block: 'b-help-link',
        mods: { type: 'modal' },
        width: 710,
        height: 620,
        stretched: true,
        url: u.getHelpUrl('remote-trading'),
        text: 'info'
    }
```

###Блок в виде текстовой псевдоссылки + иконка (?) (по умолчанию, иконка справа):###
```

    {
        block: 'b-help-link',
        mods: { type: 'modal' },
        width: 710,
        height: 620,
        stretched: true,
        url: u.getHelpUrl('remote-trading'),
        text: 'info',
        icon: 'question'
    }
```

###Блок в виде текстовой псевдоссылки + иконка (?) (иконка слева):###
```

    {
        block: 'b-help-link',
        mods: { type: 'modal', icon: 'left' },
        width: 710,
        height: 620,
        stretched: true,
        url: u.getHelpUrl('remote-trading'),
        text: 'info',
        icon: 'question'
    }
```

###Блок в виде иконки предупреждения без текста:###
```

    {
        block: 'b-help-link',
        width: 710,
        height: 620,
        stretched: true,
        url: u.getHelpUrl('remote-trading'),
        icon: 'notice'
    }
```
