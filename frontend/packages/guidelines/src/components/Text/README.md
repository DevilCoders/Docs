Компонент для представления любых текстовых сущностей.

### Свойства компонента Text

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` `left` `right` | Выравнивание |
| `textDecoration` | `underline` | Тип декорирования шрифта |
| `display` | `block` `inline` `inline-block` | Вариант отображения |
| `indent` | `xxxs` `xxs` `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl` | Размер внешнего отстпуа вниз |
| `size`  | `xs` `s` `m` `l` `xl` `xxl` `xxxl` `xxxxl`| Размер |
| `letterSpacing` | `xs` `s` `m` | Расстояние между буквами |
| `fontStyle` | `italic` | Стиль шрифта |
| `transform` | `uppercase` | Вид трансформации |
| `type` | `blockquote` `h1` `h2` `h3` `p` | Тип |
| `view` | `alert` `brand` `disable` `ghost` `link` `link-minor` `personal` `primary` `promo` `secondary` `success` `warning` | Вид отображения |
| `weight` | `bold` `light` `regular` `semibold` `thin` | Жирность |
| `isBlockElement` | `true` | Возвращает компонент в div, по-умолчанию в span |

```jsx
<Text
	align='right'
	textDecoration='underline'
	display='block'
	indent='xxxxl'
	size='l'
	letterSpacing='m'
	fontStyle='italic'
	transform='uppercase'
	type='blockquote'
	view='brand'
	weight='thin'
>
	Люк, я твой отец
</Text>
```
