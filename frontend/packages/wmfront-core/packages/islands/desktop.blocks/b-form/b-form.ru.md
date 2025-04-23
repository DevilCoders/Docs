**Статус блока**: deprecated.

**NB** Поддержка блока прекращена. В версии 6.0 будет удален.

## Описание

Форма – тег `<form>` с атрибутом `method=post` по умолчанию.

```js
{
    block: 'b-form',
    attrs: {action: '#!/action/'},
    content: [
        {
            block: 'b-form-input',
            mods: {theme: 'grey'},
            content: {
                elem: 'input',
                attrs: {
                    name: 'input_name',
                    value: 'Значение поля'
                }
            }
        },
        {
            block: 'b-form-button',
            mods: {theme: 'grey-s', size: 's'},
            type: 'submit',
            content: 'Я.кнопка'
        }
    ]
}
```
