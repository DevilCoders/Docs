## Контрол рейтинга
Предоставляет выбор оценки в виде звезд.

### Песочница
```js noeditor
<Helper.Playground component={RatingControl} />
```

### Примеры
```jsx
import Title from '@self/root/src/uikit/components/Title';

const [value, setValue] = React.useState(0);

const onChangeValue = value => setValue(value);

<div>
    <div>
        <Title size="s">
            По умолчанию
        </Title>
        <RatingControl
            name="default"
            onChange={onChangeValue}
            value={value}
        />
    </div>
    <br/>
    <div>
        <Title size="s">
            Варианты размеров (xs, s, m, l, 3xl)
        </Title>
        <RatingControl
            size="xs"
            name="size-xs"
            onChange={onChangeValue}
            value={value}
        />
        <br/>
        <br/>
        <RatingControl
            size="s"
            name="size-s"
            onChange={onChangeValue}
            value={value}
        />
        <br/>
        <br/>
        <RatingControl
            size="m"
            name="size-m"
            onChange={onChangeValue}
            value={value}
        />
        <br/>
        <br/>
        <RatingControl
            size="l"
            name="size-l"
            onChange={onChangeValue}
            value={value}
        />
        <br/>
        <br/>
        <RatingControl
            size="3xl"
            name="size-l"
            onChange={onChangeValue}
            value={value}
        />
    </div>
</div>
```
