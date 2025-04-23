# Блок social-icon2

Блок иконкон социальных сетей и мессенджеров, реагирующий на изменение Темы

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `name` | `twitter`, ...  | **Обязательный**. Имя соц. сети или мессенджера |
| `round` | `alert` `brand` `disable` `ghost` `primary` `secondary` `success` `system` `warning` | Тип скругления |
| `view` | `alert` `brand` `default` `ghost` `success` `warning` | Тип отображения |
| `size` | `m` | **Обязательный**. Размер |

```js
{
	block: 'social-icon2',
	mods: { 'name': 'twitter', view: 'primary', round: 'default' size: 'm' }
}
```
