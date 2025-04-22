**Важно**: скорее всего вам нужен не этот блок, а `m-button-action_type_phone`

Использование

```js
{
    block: 'b-form-button',
    mods: { type: 'simple', theme: 'simple-grey', size: 's' },
    mix: [{
        block: 'mi-phone-button',
        js: { phone: '777' }
    }],
    content: 'Позвонить по номеру 777'
}
```
