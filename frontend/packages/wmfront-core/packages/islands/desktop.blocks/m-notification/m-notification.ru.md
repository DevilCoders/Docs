
## m-notification

Блок — уведомление для пользователя.

### Модификаторы

- `autoclosable`('yes'/'') — определяет, будет ли уведомление автоматически закрываться по клику не на него.
- `clear`('yes'/'') — определяет, показывать ли внутри уведомления крестик, по клику на который будет закрываться уведомление.
- `icons`('yes'/'') — определяет, будет и показываться внутри уведомления иконка, соответствующая его типу.
- `theme`('error', 'warning', 'success', 'info') — определяет тип уведомления (тип иконки и цветовое оформление).

### JS-параметры
`delay`(необязательный): Number. Определяет время в миллисекундах, через которое уведомление будет автоматически закрыто после своего появления.

### События

`remove` - генерируется, когда уведомление удаляется из DOM-дерева.
