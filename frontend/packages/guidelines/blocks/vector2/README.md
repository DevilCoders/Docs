# vector2

Блок для векторной графики, поддерживиающей смысловой контент. Реагирует на тему

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `name` | `cashback`, `connect`, `discount`,`fastpay`... |  **Обязательный**. Имя иконки |
| `size` | `m` | **Обязательный**. Размер иконки |
| `view` | `alert` `disable` `ghost` `primary` `secondary` `success` `system` `warning` | Цвет отображения иконки |

```js
{
	block: 'vector2',
	mods: { name: 'cashback', size: 'm', view: 'alert' }
}
```

#### Список всех иконок
http://yamoney.design
