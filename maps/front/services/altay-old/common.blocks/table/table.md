# table

```js
{
    block: 'table',
    mods: { type: 'menu' },
    content: [
        {
            elem: 'head',
            content: [
                '', // столбец без заголовка для чекбокса
                'ID изменения',
                'Время изменения',
                'Изменения в полях'
            ]
        },
        {
            elem: 'row',
            content: [
                {
                    block: 'checkbox',
                    mods: { theme: 'islands', size: 'm' },
                    name: 'commitId',
                    val: 'yes'
                },
                {
                    block: 'link',
                    mods: { theme: 'islands' },
                    target: '_blank',
                    url: 'https://yandex.ru',
                    content: 'historyItemId'
                },
                '2015-09-23 05:44',
                'Название, адрес, телефон'
            ]
        }
    ]
}
```

```javascript
{
    block: 'table',
    mods: { type: 'menu' },
    content: [
        {
            elem: 'head',
            content: [
                '', // столбец без заголовка для чекбокса
                i18n('changelog', 'id-change'), // ID изменения
                i18n('changelog', 'time-change'), // Время изменения
                i18n('changelog', 'changed-area') // Изменения в полях
            ]
        },
        {
            elem: 'row',
            content: [
                {
                    block: 'checkbox',
                    mods: { theme: 'islands', size: 'm' },
                    name: 'commitId',
                    val: historyItemId
                },
                {
                    block: 'link',
                    mods: { theme: 'islands' },
                    target: '_blank',
                    url: '_____basePath_____/cards/' + innerId + '?commitId=' + historyItemId,
                    js: {
                        innerId: innerId
                    },
                    content: historyItemId
                },
                moment(historyItem.date).format('YYYY-MM-DD HH:mm'), // 2015-09-23 05:44
                'Название, адрес, телефон'
            ]
        }
    ]
}
```
