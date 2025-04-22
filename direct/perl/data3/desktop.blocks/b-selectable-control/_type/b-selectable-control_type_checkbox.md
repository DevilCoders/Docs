r104151
## b-selectable-control_type_checkbox ##

## Описание ##
Блок, реализующий b-selectable-control для checkbox

## Пример ##
2 чекбокса, обрабатывающие элементы с ключами "1" и "2"
    {
        block: 'some-block',
        mix: { block: 'i-selectable' },
        content: [
            {
                block: 'checkbox',
                mods: { size: 'xs' },
                mix: [
                    {
                        block: 'b-selectable-control',
                        mods: { type: 'checkbox' },
                        js: {
                            key: 1,
                            data: { param1: 1 }
                        }
                    }
                ]
            },
            {
                block: 'checkbox',
                mods: { size: 'xs', checked: 'yes' },
                mix: [
                    {
                        block: 'b-selectable-control',
                        mods: { type: 'checkbox' },
                        js: {
                            key: 2,
                            data: { param1: 3 }
                        }
                    }
                ]
            }
        ]
    }
