Компонент, устанавливающий лейбл для управляющего элемента.

```jsx
const {search} = require('../Icon');

const select = ctx.Select({state, setState});

initialState = select.initialState;

<Container>
    <Label text="Выбрать">
        <Select value={select.value} onChange={select.onChange}>
            {select.Options}
        </Select>
    </Label>

    <Label text="Название">
        <Button>Значение</Button>
    </Label>

    <Label text="Поиск">
        <Input before={<Icon src={search} />} placeholder="Начните поиск" />
    </Label>
</Container>
```

По умолчанию, Label использует html-тег 'label', но можно задать другой тег.
Например, радиогруппа внутри Label с тегом div:

```jsx
const Button = require('../RadioGroup/Items/Button').default;

const radioGroup = ctx.RadioGroup({state, setState, checked: 'DAY'});

const {initialState, onRadioGroupItemChange} = radioGroup;
<Label text="Group by" Tag="div">
    <RadioGroup onRadioGroupItemChange={onRadioGroupItemChange} checked={state.checked}>
        <Button value="DAY">Day</Button>
        <Button value="MONTH">Month</Button>
        <Button value="YEAR">Year</Button>
    </RadioGroup>
</Label>
```