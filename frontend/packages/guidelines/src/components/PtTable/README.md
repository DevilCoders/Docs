Паттерн для создания простых плоских таблиц. Набор модификаторов покрывает максимальное количество как стилистических так и структурных потребностей. Также есть возможность маркеровать строки по статусу.

Для вложенных компонентов наследуется структура как в BEM + переопределение тем/цветов:

### Свойства компонента PtTable

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `default` `ghost` | Тип отображения |
| `border` | `all` | Добавление рамок |

### Свойства компонента PtTable.Row

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `head` | Тип отображения как заголовка |
| `border` | `bottom` `top` | Добавление рамок |
| `stripe` | `even` | Полосатость |
| `status` | `default` `error` `success` `warnings` | Статус |
| `spaceV` | `xs` `s` `m` `l` | Внутренние отступы по вертикали  |
| `spaceH` | `xs` `s` `m` `l` | Внутренние отступы по горизонтали |
| `spaceA` | `xs` `s` `m` `l` | Внутренние отступы по всем сторонам |

### Свойства компонента PtTable.Column

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `width` | `5` `10` ... `100` | Ширина в процентах |
| `align` | `center` `right` | Выравнивание |

```jsx
<PtTable view='ghost' border='all'>
	<PtTable.Row view='head' border='bottom' spaceA='m'>
		<PtTable.Column width='40'>
			First row
		</PtTable.Column>
		<PtTable.Column width='60'>
			First row
		</PtTable.Column>
	</PtTable.Row>
	<PtTable.Row border='bottom' spaceA='m'>
		<PtTable.Column width='40'>
			Second row with bottom border
		</PtTable.Column>
		 <PtTable.Column width='60'>
			Second row with bottom border
		</PtTable.Column>
	</PtTable.Row>
</PtTable>
```

### Пример использование паттерна

```jsx
<div>
	<PtTable view='default' border='all' spaceH='xs' >
		<PtTable.Row view='head' border='bottom'>
			<PtTable.Column width='25' spaceH='m' spaceV='m'>
				<Text size='s' view='ghost' transform='uppercase'>
					Cat
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25' spaceH='m' spaceV='m'>
				<Text size='s' view='ghost' transform='uppercase'>
					Origin
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25' spaceH='m' spaceV='m'>
				<Text size='s' view='ghost' transform='uppercase'>
					Coat
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25' spaceH='m' spaceV='m' align='right'>
				<Text size='s' view='ghost' transform='uppercase'>
					Price
				</Text>
			</PtTable.Column>
		</PtTable.Row>
		<PtTable.Row spaceH='m' spaceV='l' border='bottom'>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					British
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Natural
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Long
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25' align='right'>
				<Text size='m' view='primary'>
					1000 ₽
				</Text>
			</PtTable.Column>
		</PtTable.Row>	
		<PtTable.Row spaceH='m' spaceV='l' border='bottom'>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Munchkin
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Mutation
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Short
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25' align='right'>
				<Text size='m' view='primary'>
					1000 ₽
				</Text>
			</PtTable.Column>
		</PtTable.Row>
		<PtTable.Row spaceH='m' spaceV='l' border='bottom'>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Maine Coon
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Natural
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Long
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25' align='right'>
				<Text size='m' view='primary'>
					3000 ₽
				</Text>
			</PtTable.Column>
		</PtTable.Row>
		<PtTable.Row spaceH='m' spaceV='l' border='bottom'>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Scottish Fold
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Natural
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Short
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25' align='right' align='right'>
				<Text size='m' view='primary'>
					3000 ₽
				</Text>
			</PtTable.Column>
		</PtTable.Row>
	</PtTable>
</div>
```

```jsx
<div>
	<PtTable view='default' stripe='even'>
		<PtTable.Row status='default' spaceH='m' spaceV='l'>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					British
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Natural
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Long
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Price
				</Text>
			</PtTable.Column>
		</PtTable.Row>	
		<PtTable.Row status='success' spaceH='m' spaceV='l'>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Munchkin
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Mutation
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Short
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					United States
				</Text>
			</PtTable.Column>
		</PtTable.Row>
		<PtTable.Row status='warning' spaceH='m' spaceV='l'>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Maine Coon
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Natural
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Long
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					United States
				</Text>
			</PtTable.Column>
		</PtTable.Row>
		<PtTable.Row status='error' spaceH='m' spaceV='l'>
			<PtTable.Column width='25'>
				<Text size='m' view='default' >
					Scottish Fold
				</Text>
			</PtTable.Column>
			 <PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Natural
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Short
				</Text>
			</PtTable.Column>
			<PtTable.Column width='25'>
				<Text size='m' view='primary'>
					Scotland
				</Text>
			</PtTable.Column>
		</PtTable.Row>
	</PtTable>
</div>
```
