Паттерн для представления информации в маленьком формате.

### Свойства компонента PtCard

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `default` | Тип отображения |
| `border` | `all` | Добавление рамок |
| `shadow` | `cloud` | Добавление тени |

### Свойства компонента PtCard.Header

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` `right` | Выравнивание сожержимого по горизонтали |
| `spaceV` | `xs` `s` `m` `l` `xl` `xxl` | Размер вертикального паддинга |
| `spaceH` | `xs` `s` `m` `l` `xl` `xxl` | Размер горизонтального паддинга |
| `spaceA` | `xs` `s` `m` `l` `xl` `xxl` | Размер всех паддингов |

### Свойства компонента PtCard.Content

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` `right` | Выравнивание сожержимого по горизонтали |
| `verticalAlign` | `center` | Выравнивание по высоте |
| `spaceT` | `xs` `s` `m` `l` `xl` `xxl` | Размер верхнего паддинга |
| `spaceR` | `xs` `s` `m` `l` `xl` `xxl` | Размер правого паддинга |
| `spaceL` | `xs` `s` `m` `l` `xl` `xxl` | Размер левого паддинга |
| `spaceB` | `xs` `s` `m` `l` `xl` `xxl` | Размер нижнего паддинга |
| `spaceV` | `xs` `s` `m` `l` `xl` `xxl` | Размер вертикального паддинга |
| `spaceH` | `xs` `s` `m` `l` `xl` `xxl` | Размер горизонтального паддинга |
| `spaceA` | `xs` `s` `m` `l` `xl` `xxl` | Размер всех паддингов |

### Свойства компонента PtCard.Footer

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` `right` | Выравнивание сожержимого по горизонтали |
| `distribute` | `between` | Расположение |
| `spaceV` | `xs` `s` `m` `l` `xl` `xxl` | Размер вертикального паддинга |
| `spaceH` | `xs` `s` `m` `l` `xl` `xxl` | Размер горизонтального паддинга |
| `spaceA` | `xs` `s` `m` `l` `xl` `xxl` | Размер всех паддингов |

### Свойства компонента PtCard.Image

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `size` | `cover` | Выравнивание сожержимого по горизонтали |
| `shadow` | `bottom-default` `bottom-inverse` `top-default` `top-inverse` | Тень поверх изображения |

```jsx
<PtCard
	view='default'
	border='all'
	shadow='cloud'
>
	<PtCard.Image>
		Image
	</PtCard.Image>
	<PtCard.Header>
		Header
	</PtCard.Header>
	<PtCard.Content spaceV='xl'>
		Content
	</PtCard.Content>
	<PtCard.Footer>
		Footer
	</PtCard.Footer>
</PtCard>
```

### Пример использование паттерна

```jsx
var demoStyles = {
	width: '270px',
	height: '330px'
};

<PtCard view='default' border='all' shadow='cloud' style={demoStyles}>
	<PtCard.Header spaceA='xl'>
		<BrandLogo name='megafon' size='m' />
	</PtCard.Header>
	<PtCard.Footer spaceA='xl'>
		<Text>
			<Decorator indentB='xs'>
				<Text size='s' view='ghost' transform='uppercase' letterSpacing='s' display='block'>
					МВидео
				</Text>
			</Decorator>
			<Decorator indentB='xs'>
				<Text size='l' view='primary' weight='bold' display='block'>
					Кэшбэк до 18%
				</Text>
			</Decorator>
			<Text size='m' view='primary' display='block'>
				Скидки до 50% на топ-бренды с М.Купонами
			</Text>
		</Text>
	</PtCard.Footer>
</PtCard>
```


```jsx
var demoStyles = {
	width: '400px',
	height: '280px',
};

<PtCard view='default' border='all' shadow='cloud' style={demoStyles}>
	<PtCard.Header spaceA='xl'>
		<PtIconPlus distribute='between' verticalAlign='center'>
			<PtIconPlus.Icon indentR='s'>
				<BrandLogo name='mts' size='m' />	
			</PtIconPlus.Icon>
			<PtIconPlus.Block>
				<Text size='m' view='primary'>
					Услуга заблокирована
				</Text>
				<Text size='m' view='primary'>
					Услуга заблокирована
				</Text>
			</PtIconPlus.Block>
		</PtIconPlus>
	</PtCard.Header>
	<PtCard.Footer spaceA='xl'>
		<Text>
			<Decorator indentB='xs'>
				<Text size='l' view='primary' weight='bold' display='block'>
					Скидка 50% на Интернет
				</Text>
			</Decorator>
			<Decorator indentB='s'>
				<Text size='m' view='primary' display='block'>
					Интернет по выгодной цене, без ограничений по времени и скорости, а округление трафика происходит с точностью до 250 КБ.
				</Text>
			</Decorator>
			<Text size='m' view='primary' transform='uppercase'>
				Подключить скидку
			</Text>
		</Text>
	</PtCard.Footer>
</PtCard>
```
