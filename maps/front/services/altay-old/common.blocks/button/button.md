# button

Расширяет `button` из `bem-components`.

## button_type_clear

При клике эмитит событие `form-clear`, на которое форма должна очистить себя.

```js
{
    block: 'button',
    mods: { theme: 'islands', size: 'm', type: 'clear' },
    text: 'Очистить форму'
}
```

## button_type_reset

Создает кнопку с атрибутом `type="reset"`.

```js
{
    block: 'button',
    mods: { theme: 'islands', size: 'm', type: 'reset' },
    text: 'Сбросить форму к исходным значениям'
}
```
