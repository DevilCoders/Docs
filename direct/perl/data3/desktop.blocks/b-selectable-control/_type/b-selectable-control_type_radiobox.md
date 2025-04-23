r104151
## b-selectable-control_type_radiobox ##

## Описание ##
Блок, реализующий b-selectable-control для radiobox

## Пример ##
Радиобокс, обрабатывающий элементы с ключами "1" и "2"

    {
        block: 'some-block',
        mix: { block: 'i-selectable' },
        content: [
            {
                block: 'radiobox',
                mods: { size: 'xs' },
                mix: [
                    {
                        block: 'b-selectable-control',
                        mods: { type: 'radiobox' },
                        js: {
                            items: {
                                1: { param1: 1 },
                                2: { param1: 2 }
                            }
                        }
                    }
                ]
            }
        ]
    }
