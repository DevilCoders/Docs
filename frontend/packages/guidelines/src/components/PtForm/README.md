Паттерн используется для представления информации, требующей ввода данных или выбора настроек, для дальнейшей отправки.

### Свойства компонента PtForm

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `ghost` `default` | Тип отображения |
| `border` | `all` | Добавление рамок |
| `shadow` | `cloud` | Добавление тени |

### Свойства компонента PtForm.Item

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `border` | `all` `bottom` `top` | Обводка |
| `spaceT` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внутренний отступ сверху |
| `spaceR` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внутренний отступ справа |
| `spaceL` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внутренний отступ слева |
| `spaceB` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внутренний отступ внизу |
| `spaceV` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внутренние отступы по вертикали |
| `spaceH` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внутренние отступы по горизонтали |
| `spaceA` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внутренние отступы по всем сторонам |
| `indentT` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ сверху |
| `indentR` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ справа |
| `indentL` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ слева |
| `indentB` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ внизу |
| `indentV` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по вертикали |
| `indentH` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по горизонтали |
| `indentA` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по всем сторонам |
| `distribute` | `between` `default` `right` | Распределение контента по горизонтали |
| `verticalAlign` | `default` `center` `baseline` | Выравнивание контента по вертикали |

### Свойства компонента PtForm.Label

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `width` | `default` `inverse` | Ширина элемента 35% / 65% относительно строки |

```jsx
<PtForm view='default' border='all' shadow='cloud' >
	<PtForm.Item spaceA='s' verticalAlign='center'>
		<PtForm.Label width='default'> Label </PtForm.Label>
		Content
	</PtForm.Item>
</PtForm>
```

### Пример использование паттерна

```jsx
var demoStyles = {
	width: '440px'
};

<PtForm view='default' border='all' style={demoStyles}>
	<PtForm.Item spaceA='xl'>
		<Text size='xl' view='primary' weight="bold">
			Персональные данные
		</Text>
	</PtForm.Item>
	<PtForm.Item spaceH='xl'>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Имя
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Адрес
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Почта
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Телефон
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
	</PtForm.Item>
	<PtForm.Item spaceA='xl' verticalAlign='center' distribute='between'>
		<Text size='m' view='link'>
			Дополнительная информация
		</Text>
		<input type="submit" value="Submit" />
	</PtForm.Item>
</PtForm>
```

```jsx
var demoStyles = {
	width: '440px'
};

<PtForm view='default' border='all' style={demoStyles}>
	<PtForm.Item spaceA='l' border='bottom'>
		<Text size='xl' view='primary' weight="bold">
			Персональные данные
		</Text>
	</PtForm.Item>
	<PtForm.Item spaceA='l' border='bottom'>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Телефон
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Имя
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Почта
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
	</PtForm.Item>
	<PtForm.Item spaceA='l' border='bottom'>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Почта
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
		<PtForm.Item spaceB='l' verticalAlign='center'>
			<PtForm.Label width='default'>
				<Text size='m' view='primary'>
					Адрес
				</Text>
			</PtForm.Label>
			<input type="text" name="name" />
		</PtForm.Item>
	</PtForm.Item>
	<PtForm.Item spaceA='l' verticalAlign='center' distribute='between' border='bottom'>
		<Text size='m' view='ghost'>
			Дополнительная информация
		</Text>
		<input type="submit" value="Submit" />
	</PtForm.Item>
</PtForm>
```

```jsx
var demoStyles = {
	width: '440px',
};

<PtForm view='default' border='all' style={demoStyles}>
	<PtForm.Item spaceA='l' border='bottom'>
		<Text size='xl' view='primary' weight="bold">
			Персональные данные
		</Text>
	</PtForm.Item>
	<PtForm.Item spaceH='l' border='bottom'>
		<PtForm.Item spaceV='l' border='bottom'>
			<PtForm.Item spaceB='l' verticalAlign='center'>
				<Text size='s' view='primary' weight='bold' letterSpacing='s' transform='uppercase'>
					Личные данные
				</Text>
			</PtForm.Item>
			<PtForm.Item spaceB='l' verticalAlign='center'>
				<PtForm.Label width='default'>
					<Text size='m' view='primary'>
						Телефон
					</Text>
				</PtForm.Label>
				<input type="text" name="name" />
			</PtForm.Item>
			<PtForm.Item spaceB='l' verticalAlign='center'>
				<PtForm.Label width='default'>
					<Text size='m' view='primary'>
						Имя
					</Text>
				</PtForm.Label>
				<input type="text" name="name" />
			</PtForm.Item>
			<PtForm.Item spaceB='l' verticalAlign='center'>
				<PtForm.Label width='default'>
					<Text size='m' view='primary'>
						Почта
					</Text>
				</PtForm.Label>
				<input type="text" name="name" />
			</PtForm.Item>
		</PtForm.Item>
		<PtForm.Item border='bottom' spaceV='l'>
			<PtForm.Item spaceB='l' verticalAlign='center'>
				<Text size='s' view='primary' weight='bold' letterSpacing='s' transform='uppercase'>
					Данные компании
				</Text>
			</PtForm.Item>
			<PtForm.Item spaceB='l' verticalAlign='center'>
				<PtForm.Label width='default'>
					<Text size='m' view='primary'>
						Почта
					</Text>
				</PtForm.Label>
				<input type="text" name="name" />
			</PtForm.Item>
			<PtForm.Item spaceB='l' verticalAlign='center'>
				<PtForm.Label width='default'>
					<Text size='m' view='primary'>
						Адрес
					</Text>
				</PtForm.Label>
				<input type="text" name="name" />
			</PtForm.Item>
		</PtForm.Item>
	</PtForm.Item>
	<PtForm.Item spaceA='l' verticalAlign='center' distribute='between' border='bottom'>
		<Text size='m' view='ghost'>
			Дополнительная информация
		</Text>
		<input type="submit" value="Submit" />
	</PtForm.Item>
</PtForm>
```
