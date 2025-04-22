# office-domik

```js
({
    block: 'office-domik',
    content: [
        {
            elem: 'text',
            content: 'Для начала работы, пожалуйста, войдите в систему:'
        },
        {
            block: 'button',
            mods: { theme: 'islands', size: 'm' },
            mix: { block: 'office-domik', elem: 'login' },
            text: 'Вход'
        }
    ]
})
```
