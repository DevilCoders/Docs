Паттрен располагающий графический элемент, например, иконку рядом с контентом.

### Свойства компонента PtIconPlus

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `distribute` | `between` `right` | Распределение контента по горизонтали |
| `verticalAlign` | `center` `top` `bottom` | Вертикальное выравнивание |

### Свойства компонента PtIconPlus.Icon

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `indentR` | `xxs` `xs` `s` `m` `l` | Отступ между иконкой и контентом справа |
| `indentL` | `xxs` `xs` `s` `m` `l` | Отступ между иконкой и контентом слева |
| `offset` | `no` | Отступ между иконкой и контентом сверху|

```jsx
<PtIconPlus verticalAlign='center'>
	<PtIconPlus.Icon indentR='l'> Icon </PtIconPlus.Icon>
	<PtIconPlus.Block> Block </PtIconPlus.Block>
</PtIconPlus>
```

### Пример использование паттерна

```jsx
<PtIconPlus verticalAlign='center'>
	<PtIconPlus.Icon indentR='s'>
		<Icon name='lock-circle' size='m' view='primary' />
	</PtIconPlus.Icon>
	<PtIconPlus.Block>
		<Text size='m' view='primary'>
			Услуга заблокирована
		</Text>
	</PtIconPlus.Block>
</PtIconPlus>
```

```jsx
<PtIconPlus distribute='between' verticalAlign='center'>
	<PtIconPlus.Block>
		<Text size='m' view='primary'>
			Услуга заблокирована
		</Text>
	</PtIconPlus.Block>
	<PtIconPlus.Icon>
		<Icon name='lock-circle' size='m' view='primary' />
	</PtIconPlus.Icon>
</PtIconPlus>
```

