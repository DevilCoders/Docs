## Рейтинг
Отображает рейтинг/оценку в виде звезд.

### Песочница
```js noeditor
<Helper.Playground component={Rating} />
```

### Примеры
```jsx
import Title from '@self/root/src/uikit/components/Title';
const DropdownNative = require('@self/root/src/uikit/components/DropdownNative').default;

const [value, setValue] = React.useState(3)

const onChangeSelector = ({currentTarget: {value}}) => setValue(value);

const getValue = () => value;

const options = [0, 1, 2, 3, 4, 4.2, 4.5, 4.8, 5].map(value => ({text: value, value}));

<div style={{position: 'relative'}}>
    <div>
        Оценка
        {' '}
        <DropdownNative options={options} onChange={onChangeSelector} value={getValue()}/>
    </div>
    <br/>
    <div>
        <Title size="s">
            По умолчанию
        </Title>
        <Rating value={getValue()} />
    </div>
    <br/>
    <div>
        <Title size="s">
            Варианты размеров (xs, s, m, l)
        </Title>
        <Rating value={getValue()} size="xs" />
        <br/>
        <br/>
        <Rating value={getValue()} size="s" />
        <br/>
        <br/>
        <Rating value={getValue()} size="m" />
        <br/>
        <br/>
        <Rating value={getValue()} size="l" />
    </div>
</div>
```
