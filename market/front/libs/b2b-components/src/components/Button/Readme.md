**theme**: normal (by default)
```jsx
<Button>Нажми на меня</Button>
```

**theme**: light
```jsx
<div style={{background: '#f7f7f7', padding: '1em'}}>
    <Button theme="light">light</Button>
</div>
```

**theme**: action
```jsx
<Button theme="action">action</Button>
```

**theme**: clear
```jsx
<Button theme="clear">clear</Button>
```

**theme**: dark
```jsx
<Button theme="dark">dark</Button>
```

active
```jsx
<Button active>active</Button>
```

disabled
```jsx
<Button disabled>disabled</Button>
```

ellipsis - текст отображается в одну строку и при нехватке места заканчивается с многоточием, значение `title` по умолчанию берется `children`, но можно задать и руками, особенно это нужно делать, когда ребенком кнопки является другой элемент.
```jsx
const style = {
    maxWidth: '200px',
    height: '140px',
    display: 'flex',
    flexDirection: 'column',
    justifyContent: 'space-between'
};

<div style={style}>
    <Button ellipsis>Очень много текста, не помещается в одной кнопке</Button>
    <Button ellipsis>
        <span>span внутри кнопки, плохой title</span>
    </Button>
    <Button ellipsis title="заданный title">
        <span>span внутри кнопки, руками заданный title</span>
    </Button>
</div>
```

with some icons:
```jsx
const {expand, date, arrow, search, remove} = require('../Icon');

<Container>
    <Button icon={<Icon src={expand} />}>Expand</Button>
    <Button icon={<Icon src={date} />}>Date</Button>
    <Button icon={<Icon src={arrow} />}>Arrow</Button>
    <Button icon={<Icon src={search} />}>Search</Button>
    <Button theme="clear" icon={<Icon src={remove} />} />
</Container>
```
