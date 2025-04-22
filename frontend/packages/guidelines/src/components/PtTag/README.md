Идентификатор для категоризации, описания, поиска данных и задания внутренней структуры. В отличие от бейджа не имеет статуса.

Тег может быть информационным, а может быть ссылкой. Также тег может быть редактируемым и нет. Если тег можно редактировать, то к нему в контент можно положить контрол.

### Свойства компонента PtTag

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `default` `disable` `link` | Тип отображения |
| `size` | `s` `m` | Размер |

### Свойства компонента PtTag.Text

 -

### Свойства компонента PtTag.Delete

 -

```jsx
<div>
	<PtTag size='m' view='default'>
		<PtTag.Text>
			PtTag size m
		</PtTag.Text>
	</PtTag>
	<PtTag size='s' view='default'>
		<PtTag.Delete>
			PtTag size s
		</PtTag.Delete>
	</PtTag>
	<PtTag size='m' view='disable'>
		<PtTag.Delete>
			PtTag view disable
		</PtTag.Delete>
	</PtTag>
	<PtTag size='m' view='link'>
		<PtTag.Delete>
			PtTag view link
		</PtTag.Delete>
	</PtTag>
</div>
```
