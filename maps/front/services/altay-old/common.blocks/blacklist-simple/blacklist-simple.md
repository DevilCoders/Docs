# blacklist-simple

```js
{
	block: 'blacklist-simple',
	content: {
		block: 'blacklist-simple',
		elem: 'content',
		content: [
            {
                elem: 'section',
                content: [
                    {
                        elem: 'title',
                        content: 'Телефон: геоспам/спам'
                    },
                    '+ 7 (495) 213-82-06'
                ]
            },
			{
				block: 'button',
				mods: { theme: 'islands', size: 's'	},
				js: { type: 'user' },
				mix: {
					block: 'blacklist-simple',
					elem: 'more-button'
				},
				text: 'Подробнее'
			}
		]
	}
}
```
