Компонент для создания недельного расписания

```jsx
const {default: WeekSchedule} = require('./');

const intervals = [
    {
        day: {
            from: 'MONDAY',
            to: 'FRIDAY',
        },
        time: {
            from: 12 * 60,
            to: 18 * 60,
        },
        excludes: {
            time: [
                {
                    from: 13 * 60,
                    to: 15 * 60,
                },
                {
                    from: 16 * 60,
                    to: 17 * 60,
                },
                {
                    from: 17 * 60,
                    to: 18 * 60,
                },
                {
                    from: 19 * 60,
                    to: 20 * 60,
                },
            ],
        },
    },
];

<div>
    <WeekSchedule intervals={intervals} onChange={data => console.log(data)} />
</div>
```
