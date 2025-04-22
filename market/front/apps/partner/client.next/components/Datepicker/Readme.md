Обычный календарь

```jsx
<DatePicker value={state.datePicker} format="YYYY-MM-DD" onChange={onChange} />
```

Календарь с выбором периода

```jsx
<DatePicker range value={state.datePicker} format="YYYY-MM-DD" onChange={onChange} />
```

Календарь с максимальным диапазоном

```jsx
<DatePicker
  range
  maxRange={{amount: 6, units: 'days'}}
  value={state.datePicker}
  format="YYYY-MM-DD"
  onChange={onChange}
/>
```

Календарь с попапом.

```jsx
<DatePickerPopover range value={state.datePicker} format="YYYY-MM-DD" onChange={onChange} />
```
