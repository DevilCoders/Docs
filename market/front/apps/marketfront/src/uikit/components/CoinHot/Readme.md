### Горящий Купон с картинкой и описанием

#### size '100'
Ачивка, которую можно получить, тач.
```jsx
import dayjs from 'dayjs';
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    endDate: dayjs().add(100, 'second').toISOString(),
};

<div>
    <ViewPort width={320} height={300}>
        <Title size='200'> &lt; 375px </Title>
        <CoinHot
            size='100'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={400} height={300}>
        <Title size='200'> &ge; 375px </Title>
        <CoinHot
            size='100'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={320} height={300}>
        <Title size='200'> &lt; 375px </Title>
        <CoinHot
            size='100'
            coin={Object.assign({}, coin, { endDate: dayjs().add(100, 'minute').toISOString() })}
        />
    </ViewPort>

    <ViewPort width={400} height={300}>
        <Title size='100'> &ge; 375px </Title>
        <CoinHot
            size='100'
            coin={Object.assign({}, coin, { endDate: dayjs().add(100, 'minute').toISOString() })}
        />
    </ViewPort>

</div>
```

#### size '200'
Получение ачивки, тач.
```jsx
import dayjs from 'dayjs';
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    endDate: dayjs().add(100, 'second').toISOString(),
};

<div>
    <ViewPort width={320} height={400}>
        <Title size='200'> &lt; 375px </Title>
        <CoinHot
            size='200'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={400} height={400}>
        <Title size='200'> &ge; 375px </Title>
        <CoinHot
            size='200'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={320} height={400}>
        <Title size='200'> &lt; 375px </Title>
        <CoinHot
            size='200'
            coin={Object.assign({}, coin, { endDate: dayjs().add(100, 'minute').toISOString() })}
        />
    </ViewPort>

    <ViewPort width={400} height={400}>
        <Title size='200'> &ge; 375px </Title>
        <CoinHot
            size='200'
            coin={Object.assign({}, coin, { endDate: dayjs().add(100, 'minute').toISOString() })}
        />
    </ViewPort>

</div>
```

#### size '250'
Ачивка, которую можно получить, десктоп.
```jsx
import dayjs from 'dayjs';
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    endDate: dayjs().add(100, 'second').toISOString(),
};

<div style={{display: 'flex'}}>
    <CoinHot
        size='250'
        coin={coin}
    />

    <div style={{padding: 20}} />

    <CoinHot
        size='250'
        coin={Object.assign({}, coin, { endDate: dayjs().add(100, 'minute').toISOString() })}
    />
</div>
```

#### size '300'
Полученная ачивка (не выделенная), тач.
```jsx
import dayjs from 'dayjs';
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    endDate: dayjs().add(100, 'second').toISOString(),
};

<div>
    <ViewPort width={320} height={400}>
        <Title size='200'> &lt; 375px </Title>
        <CoinHot
            size='300'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={400} height={400}>
        <Title size='200'> &ge; 375px </Title>
        <CoinHot
            size='300'
            coin={coin}
        />
    </ViewPort>

</div>
```

#### size '400'
Полученная ачивка (выделенная), тач.
```jsx
import dayjs from 'dayjs';
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    endDate: dayjs().add(100, 'second').toISOString(),
};

<div>
    <ViewPort width={320} height={450}>
        <Title size='200'> &lt; 375px </Title>
        <CoinHot
            size='400'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={400} height={450}>
        <Title size='200'> &ge; 375px </Title>
        <CoinHot
            size='400'
            coin={coin}
        />
    </ViewPort>

</div>
```

#### size '500'
Полученная ачивка, получение ачивки, десктоп.
```jsx
import dayjs from 'dayjs';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    endDate: dayjs().add(100, 'second').toISOString(),
};

<div style={{display: 'flex'}}>
    <CoinHot
        size='500'
        coin={coin}
    />

    <div style={{padding: 20}} />

    <CoinHot
        size='500'
        coin={Object.assign({}, coin, { endDate: dayjs().add(100, 'minute').toISOString() })}
    />
</div>
```

#### theme 'black'
```jsx
import dayjs from 'dayjs';
const {$red600} = require('@self/root/src/uikit/palette/colors');

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    endDate: dayjs().add(50, 'hour').toISOString(),
};

<div style={{background: 'black', padding: 10}} >
    <CoinHot
        coin={coin}
        theme='black'
    />
</div>
```

