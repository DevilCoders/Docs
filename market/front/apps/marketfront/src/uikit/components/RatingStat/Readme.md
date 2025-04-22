## Рейтинг
Отображает одной строкой рейтинг/оценку в виде звезд и вложенный компонент

### Песочница
```js noeditor
<Helper.Playground component={RatingStat} />
```

### Примеры
```jsx
import Text from '@self/root/src/uikit/components/Text';
import Title from '@self/root/src/uikit/components/Title';
const DropdownNative = require('@self/root/src/uikit/components/DropdownNative').default;

const [value, setValue] = React.useState(3);

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
        <RatingStat value={getValue()}>
            <Text size={300} theme={'muted'}>57 отзывов</Text>
        </RatingStat>
    </div>
    <br/>
    <div>
        <Title size="s">
            Варианты размеров (xs, s, m, l)
        </Title>
        <RatingStat value={getValue()} size="xs">
            <Text size={100} theme={'muted'}>57 отзывов</Text>
        </RatingStat>
        <br/>
        <br/>
        <RatingStat value={getValue()} size="s">
            <Text size={200} theme={'muted'}>57 отзывов</Text>
        </RatingStat>
        <br/>
        <br/>
        <RatingStat value={getValue()} size="m">
            <Text size={300} theme={'muted'}>57 отзывов</Text>
        </RatingStat>
        <br/>
        <br/>
        <RatingStat value={getValue()} size="l">
            <Text size={300} theme={'muted'}>57 отзывов</Text>
        </RatingStat>
    </div>
</div>
```
