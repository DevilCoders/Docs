### Базовая реализация Купона

#### size '100'
Ачивка, которую можно получить, тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';
const {$green600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<div>
    <ViewPort width={320} height={300}>
        <Title size='200'> &lt; 375px </Title>
        <CoinBase
            size='100'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

    <ViewPort width={400} height={300}>
        <Title size='200'> &ge; 375px </Title>
        <CoinBase
            size='100'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

</div>
```

#### size '200'
Получение ачивки, тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';
const {$green600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<div>
    <ViewPort width={320} height={400}>
        <Title size='200'> &lt; 375px </Title>
        <CoinBase
            size='200'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

    <ViewPort width={400} height={400}>
        <Title size='200'> {">="} 375px </Title>
        <CoinBase
            size='200'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

</div>
```

#### size '250'
Ачивка, которую можно получить, десктоп.
```jsx
const {$green600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<CoinBase
    size='250'
    info={<Info />}
    image={<Image />}
    background={$green600}
/>
```

#### size '300'
Полученная ачивка (не выделенная), тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';
const {$green600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<div>
    <ViewPort width={320} height={400}>
        <Title size='200'> &lt; 375px </Title>
        <CoinBase
            size='300'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

    <ViewPort width={400} height={400}>
        <Title size='200'> {">="}375px </Title>
        <CoinBase
            size='300'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

</div>
```

#### size '400'
Полученная ачивка (выделенная), тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';
const {$green600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<div>
    <ViewPort width={320} height={450}>
        <Title size='200'> &lt; 375px </Title>
        <CoinBase
            size='400'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

    <ViewPort width={400} height={450}>
        <Title size='200'> {">="}375px </Title>
        <CoinBase
            size='400'
            info={<Info />}
            image={<Image />}
            background={$green600}
        />
    </ViewPort>

</div>
```

#### size '500'
Полученная ачивка, получение ачивки, десктоп.
```jsx
const {$green600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<CoinBase
    size='500'
    info={<Info />}
    image={<Image />}
    background={$green600}
/>
```

#### background 'red'
```jsx
const {$red600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<CoinBase
    size='100'
    info={<Info />}
    image={<Image />}
    background={$red600}
/>
```

#### fade 'true'
```jsx
const {$red600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<CoinBase
    size='100'
    info={<Info />}
    image={<Image />}
    background={$red600}
    fade={true}
/>
```

#### width 'auto'
```jsx
const {$red600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<div style={{resize: 'horizontal', overflow: 'hidden', padding: 10, width: 200}}>
    <CoinBase
        size='100'
        info={<Info />}
        image={<Image />}
        background={$red600}
        width='auto'
    />
</div>
```

#### theme 'black'
```jsx
const {$green600} = require('@self/root/src/uikit/palette/colors');
const {Info, Image} = require('./styleguide');

<div style={{background: 'black', padding: 10}} >
    <CoinBase
        size='100'
        info={<Info />}
        image={<Image />}
        background={$green600}
        theme='black'
    />
</div>
```
