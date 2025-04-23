Без начальных значений и ограничений

```(jsx)
initialState = {
    startDate: undefined,
    endDate: undefined,
};

const handlePeriodChange = (startDate, endDate) => {
    setState({
        startDate,
        endDate,
    });
};

<DatePicker
    startDate={state.startDate}
    endDate={state.endDate}
    onChange={handlePeriodChange}
    pastSelection={true}
/>
```

С начальными значениями и ограничениями

```(jsx)
const moment = require('moment');

initialState = {
    startDate: new Date('2019-02-07'),
    endDate: new Date('2019-02-08'),
};

const handlePeriodChange = (startDate, endDate) => {
    setState({
        startDate,
        endDate,
    });
};

<DatePicker
    minDate={new Date('2019-01-11')}
    maxDate={new Date('2019-03-21')}
    startDate={state.startDate}
    endDate={state.endDate}
    onChange={handlePeriodChange}
    showDisabledMonthNavigation
/>
```

С выбранным единственным днём и ошибкой

```(jsx)
const moment = require('moment');

initialState = {
    startDate: new Date(),
    endDate: new Date(),
};

const handlePeriodChange = (startDate, endDate) => {
    setState({
        startDate,
        endDate,
    });
};

<DatePicker
    startDate={state.startDate}
    endDate={state.endDate}
    onChange={handlePeriodChange}
    error={true}
/>
```

Можно отобразить несколько месяцев

```(jsx)
const moment = require('moment');

initialState = {
    startDate: new Date(),
    endDate: new Date(),
};

const handlePeriodChange = (startDate, endDate) => {
    setState({
        startDate,
        endDate,
    });
};

<DatePicker
    startDate={state.startDate}
    endDate={state.endDate}
    onChange={handlePeriodChange}
    fixedHeight
    monthsShown={2}
/>
```

Moжно исключить определенные даты

```(jsx)
const moment = require('moment');

initialState = {
    startDate: new Date('2019-02-07'),
    endDate: new Date('2019-02-08'),
};

const handlePeriodChange = (startDate, endDate) => {
    setState({
        startDate,
        endDate,
    });
};

<DatePicker
    startDate={state.startDate}
    endDate={state.endDate}
    onChange={handlePeriodChange}
    excludeDates={[
        new Date('2019-02-12'),
        new Date('2019-02-13'),
    ]}
/>
```

С маленькой кнопкой (buttonSize)

```(jsx)
initialState = {
    startDate: undefined,
    endDate: undefined,
};

const handlePeriodChange = (startDate, endDate) => {
    setState({
        startDate,
        endDate,
    });
};

<DatePicker
    startDate={state.startDate}
    endDate={state.endDate}
    onChange={handlePeriodChange}
    pastSelection={true}
    buttonSize='s'
/>
```
