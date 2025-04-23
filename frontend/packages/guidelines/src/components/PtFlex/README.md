Компонент для представления однострочных и многострочных секции с «плавающим» размером колонок.

### Свойства компонента PtFlex

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view`  | `stripe` | Тип отображения |
| `border` | `all` | Добавление рамок |
| `shadow` | `cloud` | Добавление тени |
| `status` | `default` `success` `warning` `alert` | Статус |
| `spaceV` | `xs` `s` `m` `l` | Размер вертикального паддинга  |
| `spaceH` | `xs` `s` `m` `l` | Размер горизонтального паддинга |
| `spaceA` | `xs` `s` `m` `l` | Размер всех паддингов |

### Свойства компонента PtFlex.Column

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` `right` | Выравнивание |
| `width` | `5` `10` ... `100` | Ширина в процентах |

```jsx
<div>
	<PtFlex view='stripe' status='warning' spaceA='m'>
		<PtFlex.Column width='30' align='center'>Column 30</PtFlex.Column>
		<PtFlex.Column width='30' align='center'>Column 30</PtFlex.Column>
		<PtFlex.Column width='40' align='center'>Column 40</PtFlex.Column>
	</PtFlex>
	<PtFlex view='stripe' status='alert' spaceA='m'>
		<PtFlex.Column width='30' align='right'>Column 30</PtFlex.Column>
		<PtFlex.Column width='30' align='right'>Column 30</PtFlex.Column>
		<PtFlex.Column width='40' align='right'>Column 40</PtFlex.Column>
	</PtFlex>
</div>
```

### Пример использование паттерна

```jsx
<div>
	<PtFlex
		view='stripe'
		shadow='cloud'
		status='success'
		spaceV='m'
		spaceH='l'
	>
		<PtFlex.Column width='20' align='left'>
			<Text size='m' view='primary' weight='bold'>5 июн 21:34</Text>
		</PtFlex.Column>
		<PtFlex.Column width='50' align='center'>
			<Text size='m' view='primary'>
				выставил счет № 56290275631 для «Yandex»
			</Text>
		</PtFlex.Column>
		<PtFlex.Column width='30' align='right'>
			<Text size='m' view='success' weight='bold'>
				30 000 ₽
			</Text>
		</PtFlex.Column>
	</PtFlex>
</div>
```
