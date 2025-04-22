r102680
# Блок b-hidden


## Подключение

```javascript
{
    block: 'b-hidden',
    // при необходимости можно выключить
    mods: { disabled: 'yes' },
    attrs: {
        name: 'my_hidden_variable',
        value: 'my_hidden_value'
    }
}
```

## Использование

```javascript
var hiddenBlock = this.findBlock...('b-hidden');

hiddenBlock.setMod('disabled', 'yes'); // чтобы исключить из отправляемых формой данных
hiddenBlock.val(hiddenBlock.val() + '_suff'); // для получения и установки значения
```
