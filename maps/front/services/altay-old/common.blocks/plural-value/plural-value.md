# plural-value

Блок-хелпер для добавления в формы контролов со множественными значениями.

## Модификаторы

### _positioning

* absolute: Элементы добавления и удаления позиционируются абсолютно
* inline: Элементы добавления и удаления позиционируются инлайново

## Пример использования

```js
{
    block: 'form',
    mix: {
        block: 'plural-value',
        mods: { positioning: 'inline' },
        js: true
    },
    content: [
        {
            // input в этом элементе можно добавлять много раз
            elem: 'elem',
            content: {
                block: 'plural-value',
                elem: 'section',
                mix: { block: 'my-block', elem: 'my-elem' }
                js: {
                    sectionMix: { block: 'my-block', elem: 'my-elem' },
                    data: {
                        block: 'input',
                        mods: { theme: 'islands', size: 'm', width: 'available', 'has-clear': true }
                    }
                },
                content: {
                    block: 'input',
                    mods: { theme: 'islands', size: 'm', width: 'available', 'has-clear': true }
                }
            }
        },
        {
            // textarea в этом элементе можно добавлять много раз
            elem: 'elem',
            content: {
                block: 'plural-value',
                elem: 'section',
                js: {
                    data: {
                        block: 'textarea',
                        mods: { theme: 'islands', size: 'm', width: 'available' }
                    }
                },
                content: {
                    block: 'textarea',
                    mods: { theme: 'islands', size: 'm', width: 'available' }
                }
            }
        },
        {
            // select в этом элементе можно добавлять много раз
            elem: 'elem',
            content: {
                block: 'plural-value',
                elem: 'section',
                js: {
                    data: {
                        block: 'select',
                        mods: { mode: 'check', theme: 'islands', size: 'm' },
                        name: 'select1',
                        val: [2],
                        text: '—',
                        options: [
                            { val: 1, text: 'Доклад' },
                            { val: 2, text: 'Мастер-класс' },
                            { val: 3, text: 'Круглый стол' }
                        ]
                    }
                },
                content: {
                    block: 'select',
                    mods: { mode: 'check', theme: 'islands', size: 'm' },
                    name: 'select1',
                    val: [2],
                    text: '—',
                    options: [
                        { val: 1, text: 'Доклад' },
                        { val: 2, text: 'Мастер-класс' },
                        { val: 3, text: 'Круглый стол' }
                    ]
                }
            }
        },
        {
            // select в этом элементе можно добавлять много раз
            elem: 'elem',
            content: {
                block: 'plural-value',
                elem: 'section',
                js: {
                    data: {
                        block: 'select',
                        mods: { mode: 'radio', theme: 'islands', size: 'm' },
                        name: 'select2',
                        val: 2,
                        options: [
                            { val: 1, text: 'Доклад' },
                            { val: 2, text: 'Мастер-класс' },
                            { val: 3, text: 'Круглый стол' }
                        ]
                    }
                },
                content: {
                    block: 'select',
                    mods: { mode: 'radio', theme: 'islands', size: 'm' },
                    name: 'select2',
                    val: 2,
                    options: [
                        { val: 1, text: 'Доклад' },
                        { val: 2, text: 'Мастер-класс' },
                        { val: 3, text: 'Круглый стол' }
                    ]
                }
            }
        },
        {
            // suggest в этом элементе можно добавлять много раз
            elem: 'elem',
            content: {
                block: 'plural-value',
                elem: 'section',
                js: {
                    data: {
                        block: 'suggest',
                        mods: {
                            'has-dataprovider': true,
                            type: 'default',
                            theme: 'islands',
                            size: 's'
                        },
                        dataprovider: {}
                    }
                },
                content: {
                    block: 'suggest',
                    mods: {
                        'has-dataprovider': true,
                        type: 'default',
                        theme: 'islands',
                        size: 's'
                    },
                    dataprovider: {}
                }
            }
        }
    ]
}
```
