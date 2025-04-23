Обычный календарь

```jsx
const {default: DatePicker} = require('./')
const {normal: {initialState, onChange}} = ctx.DatePicker({setState});

<DatePicker value={state.datePicker} format="YYYY-MM-DD" onChange={onChange} />
```

Календарь с выбором периода

```jsx
const {default: DatePicker} = require('./')
const {range: {initialState, onChange}} = ctx.DatePicker({setState});

<DatePicker range value={state.datePicker} format="YYYY-MM-DD" onChange={onChange} />
```

Календарь с максимальным диапазоном

```jsx
const {default: DatePicker} = require('./');
const {withMaxRange: {initialState, onChange}} = ctx.DatePicker({setState});

<DatePicker
  range
  maxRange={{amount: 6, units: 'days'}}
  value={state.datePicker}
  format="YYYY-MM-DD"
  onChange={onChange}
/>
```

Календарь с попапом.

**HOCS**: [withDropdown](#withdropdown).

```jsx
const DatePickerDropdown = require('./DatePickerDropdown').default;

const {range: {initialState, onChange}} = ctx.DatePicker({setState});

<DatePickerDropdown range value={state.datePicker} format="YYYY-MM-DD" onChange={onChange} />
```
