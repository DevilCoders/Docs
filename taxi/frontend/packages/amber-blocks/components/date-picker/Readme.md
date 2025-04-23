```jsx harmony
const moment = require('moment');
const currentDate = moment();
const Grid = require('../../styleguide/components/grid/Grid').default;
const Calendar = require('../icon/Calendar').default;
const Input = require('../input').default;

<Grid container spacing={2} style={{width: 600}}>
    <Grid item spacing={2} size={12}>
        Простой
    </Grid>
    <Grid item spacing={2} size={12}>
        <DatePicker
            selected={state.date || currentDate}
            onChange={(date, event) => setState({date})}
            placeholderText="Я подсказка"
            customInput={<Input iconRight={<Calendar/>} needEvent/>}
            locale="ru"
        />
    </Grid>
    <Grid item spacing={2} size={12}>
        Заблокирован
    </Grid>
    <Grid item spacing={2} size={12}>
        <DatePicker
            disabled
            selected={state.date || currentDate}
            customInput={<Input iconRight={<Calendar/>} needEvent/>}
            locale="ru"
        />
    </Grid>
</Grid>
```
