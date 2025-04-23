```js
const {default: Select, Option, OptionList} = require('../Select');
const {Unit} = require('../Grid');
const {default: Button} = require('../Button');

initialState = {value: {from: 2, to: 5}};
const onChange = ({value}) => setState({value});

<Select
  range
  value={state.value}
  onChange={onChange}
  placeholder="Выберите значение"
  submitted={({onSubmit, onCancel, disabled}) => (
    <Unit justify="space-between">
        <Button onClick={onCancel}>Отменить</Button>
        <Button disabled={disabled} look="accent" onClick={onSubmit}>Сохранить</Button>
    </Unit>
  )}
>
  <Option value={1} title="Вариант 1" />
  <Option value={2}>Вариант 2</Option>
  <Option value={3}>Третий вариант с длинным названием</Option>
  <Option value={4}>Вариант 4</Option>
  <Option value={5}>Вариант 5</Option>
  <OptionList label="Группа">
    <Option value={6}>Вариант 6</Option>
    <Option value={7}>Вариант 7</Option>
    <Option value={8}>Вариант 8</Option>
    <Option value={9}>Вариант 9</Option>
    <Option value={10}>Вариант 10</Option>
    <Option value={11}>Вариант 11</Option>
  </OptionList>
</Select>
```
