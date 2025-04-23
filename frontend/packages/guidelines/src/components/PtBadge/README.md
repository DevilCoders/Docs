Компонент для маркировки статуса сущности. Например, статус платежа.

### Свойства компонента PtBadge

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `success` `warning` `alert` `default` | Тип отображения |

```jsx
<div>
	<PtBadge view='success'>
		success
	</PtBadge>
	<PtBadge view='warning'>
		warning
	</PtBadge>
	<PtBadge view='alert'>
		alert
	</PtBadge>
	<PtBadge view='default'>
		default
	</PtBadge>
</div>
