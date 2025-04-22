# Calendar


## Базовый вариант
```js
import { Calendar as CalendarBase, withLayoutMonth } from '@yandex-int/draft-components/Datepicker/touch-phone';

const Calendar = compose(withLayoutMonth)(CalendarBase);

const App = () => {
    const [visible, setVisible] = React.useState(false);
    
    const date1 = new Date('2020-05-23');
    const date2 = new Date(date.getFullYear(), date.getMonth() + 4, 10);

    return (
        <Calendar
            layout="month"
            borders={[date, date2]}
            isDisabledItem={(date) => date.getDate() === 13}
            itemOnClick={(e) => {
                console.log(e.currentTarget.dataset.date);
            }}
        />
    );
};
```