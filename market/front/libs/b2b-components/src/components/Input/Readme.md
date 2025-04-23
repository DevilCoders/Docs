Стандартный input

```jsx
<Input placeholder="Введите текст" />
```

Со значением

```jsx
<Input placeholder="Введите текст" defaultValue="Какое-то значение" />
```

С иконкой

```jsx
const {search} = require('../Icon');

<Input before={<Icon src={search} />} placeholder="Начните поиск" />
```

С кнопкой

```jsx
<Input placeholder="Начните поиск" after={
    ({isFocused}) => (
        <Button theme={isFocused ? 'action' : 'normal'}>
            {isFocused ? 'Focused' : 'Blured'}
        </Button>
    )
} />
```
