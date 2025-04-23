Добавляет Компоненту состояние активное/неактивное и сеттеры для его управления.

```jsx
const {default: withToggle} = require('./')
const {default: Link} = require('../Link')

const Container = styled(({className, onToggle, active}) => [
  <Link onClick={onToggle}>
    {active ? 'Скрыть' : 'Раскрыть'}
  </Link>,
  active
    ? (
      <div className={className}>
        Контент
      </div>
    ) : null,
])({
  marginTop: 20
})

const Enhanced = withToggle(Container)

;
<Enhanced />
```
