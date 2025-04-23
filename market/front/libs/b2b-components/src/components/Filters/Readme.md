Компонент для расстановки контролов/фильтров контента.
```jsx
const {DatePickerDropdown} = require('../Datepicker');

const {range: datePicker} = ctx.DatePicker({state, setState});
const select = ctx.Select({state, setState});

initialState = Object.assign({}, datePicker.initialState, select.initialState);

<section>
    <Filters>
        <DatePickerDropdown range value={datePicker.value} format="YYYY-MM-DD" onChange={datePicker.onChange} />

        <Select value={select.value} onChange={select.onChange}>
            {select.Options}
        </Select>

        {false && <Button>Спрятанная кнопка, что не должна оставить пустой промежуток</Button>}

        <Button>Filter Button</Button>

        <Input placeholder="Введите текст" />
    </Filters>

    <div>Content</div>
</section>
```
