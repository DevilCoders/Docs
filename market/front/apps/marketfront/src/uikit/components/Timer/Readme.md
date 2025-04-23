
## Примеры

### Таймер

Используется для Купонов

```jsx
import dayjs from 'dayjs';

<div style={{textAlign: 'center'}}>
    <Timer endTime={dayjs().add(100, 'second').format()} />
    <Timer endTime={dayjs().add(100, 'minute').format()} />
    <Timer endTime={dayjs().add(101, 'hour').format()} />
</div>
```

#### size '100'
```jsx
import dayjs from 'dayjs';

<div style={{textAlign: 'center'}}>
    <Timer size='100' endTime={dayjs().add(100, 'second').format()} />
    <Timer size='100' endTime={dayjs().add(100, 'minute').format()} />
</div>
```

#### size '500'
```jsx
import dayjs from 'dayjs';

<div style={{textAlign: 'center'}}>
    <Timer size='500' endTime={dayjs().add(100, 'second').format()} />
    <Timer size='500' endTime={dayjs().add(100, 'minute').format()} />
</div>
```
