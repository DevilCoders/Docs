Паттерн для описание списка похожих друг на друга вертикально перечисленных сущностей.

### Свойства компонента PtList

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `default` `ghost` | Тип отображения |
| `border` | `all` | Добавление рамок |
| `shadow` | `cloud` | Добавление тени |

### Свойства компонента PtList.Item

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `border` | `bottom` `top` | рамки |
| `spaceT` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ сверху |
| `spaceR` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ справа |
| `spaceL` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ слева |
| `spaceB` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ внизу |
| `spaceV` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренние отступы по вертикали |
| `spaceH` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренние отступы по горизонтали |
| `spaceA` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренние отступы по всем сторонам |
| `indentT` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ сверху |
| `indentR` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ справа |
| `indentL` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ слева |
| `indentB` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ внизу |
| `indentV` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по вертикали |
| `indentH` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по горизонтали |
| `indentA` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по всем сторонам |
| `distribute` | `between` `default` | Распределение контента внутри PtList.Item по горизонтали |
| `verticalAlign` | `center` `top` | Выравнивание контента внутри PtList.Item по вертикали |

```jsx
<PtList border='all' view='ghost' shadow='cloud'>
	<PtList.Item verticalAlign='center' spaceA='l' border='bottom'>
		FirstItem
	</PtList.Item>
	<PtList.Item verticalAlign='center' spaceA='l' border='bottom'>
		SecondItem
	</PtList.Item>
</PtList>
```

### Пример использование паттерна

```jsx
const demoStyles = {
	width: '480px'
};

<div>
	<PtList border='all' view='default' style={demoStyles}>
		<PtList.Item spaceV='s' spaceH='l' distribute="between" verticalAlign='center' border='bottom'>
			<PtIconPlus distribute='between' verticalAlign='center'>
				<PtIconPlus.Icon indentR='s'>
					<BrandLogo name='megafon' size='s' />
				</PtIconPlus.Icon>
				<PtIconPlus.Block>
					<Text size='m' view='primary'>
						+7 921 890 80 60
					</Text>
				</PtIconPlus.Block>
			</PtIconPlus>
			<Text size='m' view='primary'>
				− 1 000 ₽
			</Text>
		</PtList.Item>
		<PtList.Item spaceV='s' spaceH='l' distribute="between" verticalAlign='center' border='bottom'>
			<PtIconPlus distribute='between' verticalAlign='center'>
				<PtIconPlus.Icon indentR='s'>
					<BrandLogo name='mts' size='s' />
				</PtIconPlus.Icon>
				<PtIconPlus.Block>
					<Text size='m' view='primary'>
						+7 910 081 45 26
					</Text>
				</PtIconPlus.Block>
			</PtIconPlus>
			<Text size='m' view='success'>
				+ 1 000 ₽
			</Text>
			</PtList.Item>
				<PtList.Item spaceV='s' spaceH='l' distribute="between" verticalAlign='center' border='bottom'>
			<PtIconPlus distribute='between' verticalAlign='center'>
				<PtIconPlus.Icon indentR='s'>
					<BrandLogo name='tele2' size='s' />
				</PtIconPlus.Icon>
				<PtIconPlus.Block>
					<Text size='m' view='primary'>
						+7 977 887 09 82
					</Text>
				</PtIconPlus.Block>
			</PtIconPlus>
			<Text size='m' view='success'>
				+ 1 000 ₽
			</Text>
		</PtList.Item>
	</PtList>
</div>
```

```jsx
const demoStyles = {
	width: '480px'
};

<div>
	<PtList border='all' view='default' style={demoStyles}>
		<PtList.Item spaceV='m' spaceH='xl' border='bottom'>
			<Text size='xl' view='primary' weight='bold'>
				Способы платежа и комиссии
			</Text>
		</PtList.Item>
		<PtList.Item spaceH='xl' spaceV='s' border='bottom'>
			<PtList.Item spaceV='s'distribute="between" verticalAlign='center' border='bottom'>
				<PtIconPlus distribute='between' verticalAlign='center'>
					<PtIconPlus.Icon indentR='s'>
						<Icon name='check' size='s' view='success' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
						<Text size='m' view='primary'>
							Яндекс.Деньги
						</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
				<Text size='m' view='primary'>
					2.2%
				</Text>
			</PtList.Item>
			<PtList.Item spaceV='s' distribute="between" verticalAlign='center' border='bottom'>
				<PtIconPlus distribute='between' verticalAlign='center'>
					<PtIconPlus.Icon indentR='s'>
						<Icon name='check' size='s' view='success' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
						<Text size='m' view='primary'>
							Банковские карты
						</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
				<Text size='m' view='primary'>
					2.3%
				</Text>
			</PtList.Item>
			<PtList.Item spaceV='s' distribute="between" verticalAlign='center' border='bottom'>
				<PtIconPlus distribute='between' verticalAlign='center'>
					<PtIconPlus.Icon indentR='s'>
						<Icon name='check' size='s' view='success' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
						<Text size='m' view='primary'>
							Баланс телефона
						</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
				<Text size='m' view='primary'>
					2.4%
				</Text>
			</PtList.Item>
			<PtList.Item spaceV='s' distribute="between" verticalAlign='center' border='bottom'>
				<PtIconPlus distribute='between' verticalAlign='center'>
					<PtIconPlus.Icon indentR='s'>
						<Icon name='check' size='s' view='success' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
						<Text size='m' view='primary'>
							Сбербанк Онлайн
						</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
				<Text size='m' view='primary'>
					2.4%
				</Text>
			</PtList.Item>
		</PtList.Item>
	</PtList>
</div>
```
