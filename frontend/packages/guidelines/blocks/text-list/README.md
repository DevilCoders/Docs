# text-list

Блок для представления текстового списка.

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `type` | `bullet` | Тип списка |

### Элементы блока
 
| Элемент | Описание |
| --------| -------- |
| `item` | Пунт списка |

```js
{
	block: 'textlist',
	mods: { type: 'bullet' },
	content: [
		{
			elem: 'item',
			content: '1'
		},
		{
			elem: 'item',
			content: '2'
		},
		{
			elem: 'item',
			content: '3'
		}
	]
}
```
