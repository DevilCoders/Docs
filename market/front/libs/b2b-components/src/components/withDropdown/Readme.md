Добавляет Компоненту поведение дропдауна.

```jsx
const {default: withDropdown} = require('./')

const Content = styled(({className}) => (
  <div className={className}>Контент</div>)
)({padding: 50})

const Enhanced = withDropdown(Content)

;
<Enhanced placeholder="Нажми на меня" />
```
