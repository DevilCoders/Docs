# text

В основе любого интерфейса лежит типографика. Блок для представления любых текстовых сущностей.

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` `left` `right` | Выравнивание |
| `decoration` | `underline` | Тип декорирования шрифта |
| `display` | `block` `inline` `inline-block` | Вариант отображения |
| `indent` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` | Размер внешнего отстпуа вниз |
| `size`  | `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl`| Размер |
| `spacing` | `xs` `s` `m` | Расстояние между буквами |
| `style` | `italic` | Стиль шрифта |
| `transform` | `uppercase` | Вид трансформации |
| `type` | `blockquote` `h1` `h2` `h3` `p` | Тип |
| `view` | `alert` `brand` `disable` `ghost` `link` `link-minor` `personal` `primary` `promo` `secondary` `success` `warning` | Вид отображения |
| `weight` | `bold` `light` `regular` `semibold` `thin` | Жирность |

```js
{
	block: 'text',
	mods: { view: 'primary', size: 'm', weight: 'bold' }
	content: 'Люк, я твой отец'
}
```
