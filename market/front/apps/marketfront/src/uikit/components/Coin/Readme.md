### Купон с картинкой и описанием

#### size 'auto'
Ачивка, которую можно получить, тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};
const coinWithTimer = {
 "id": 155866506,
 "subtitle": "на товары для водоснабжения от 3 000 ₽",
 "type": "FIXED",
 "description": "Полезный Маркет Бонус! С ним вы можете сэкономить 300 ₽, когда будете покупать товары для водоснабжения от 3 000 ₽. Кстати, использовать эту скидку можно вместе с другими Маркет Бонусами.",
 "images": {
  "standard": "https://avatars.mds.yandex.net/get-smart_shopping/1546391/8ed3b42b-aef0-4492-8c18-65f33f4a45fe/"
 },
 "status": "ACTIVE",
 "reason": "FOR_USER_ACTION",
 "title": "Скидка 300 ₽",
 "endDate": "2020-03-31T20:59:59.000Z",
 "creationDate": "2020-02-21T04:17:21.000Z",
 "nominal": {
  "value": 300,
  "currency": "RUR"
 },
 "backgroundColor": "#b3b3b3",
 "restrictions": [
  {
   "restrictionType": "CATEGORY",
   "msku": null,
   "categoryId": 16207941
  }
 ]
};

<div>
    <ViewPort width={320} height={300}>
        <div style={{display: 'flex', justifyContent: 'space-around'}}>
            <Coin
                size='auto'
                coin={coin}
            />
            <Coin
                size='auto'
                coin={coinWithTimer}
            />
        </div>
    </ViewPort>
</div>
```

#### size '50'
Ачивка, которую можно получить, тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};
const coinWithTimer = {
 "id": 155866506,
 "subtitle": "на товары для водоснабжения от 3 000 ₽",
 "type": "FIXED",
 "description": "Полезный Маркет Бонус! С ним вы можете сэкономить 300 ₽, когда будете покупать товары для водоснабжения от 3 000 ₽. Кстати, использовать эту скидку можно вместе с другими Маркет Бонусами.",
 "images": {
  "standard": "https://avatars.mds.yandex.net/get-smart_shopping/1546391/8ed3b42b-aef0-4492-8c18-65f33f4a45fe/"
 },
 "status": "ACTIVE",
 "reason": "FOR_USER_ACTION",
 "title": "Скидка 300 ₽",
 "endDate": "2020-03-31T20:59:59.000Z",
 "creationDate": "2020-02-21T04:17:21.000Z",
 "nominal": {
  "value": 300,
  "currency": "RUR"
 },
 "backgroundColor": "#b3b3b3",
 "restrictions": [
  {
   "restrictionType": "CATEGORY",
   "msku": null,
   "categoryId": 16207941
  }
 ]
};

<div>
    <ViewPort width={320} height={300}>
        <Title size='200'> &lt; 375px </Title>
        <div style={{display: 'flex', justifyContent: 'space-around'}}>
            <Coin
                size='50'
                coin={coin}
            />
            <Coin
                size='50'
                coin={coinWithTimer}
            />
        </div>
    </ViewPort>

</div>
```

#### size '100'
Ачивка, которую можно получить, тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};
const coinWithTimer = {
 "id": 155866506,
 "subtitle": "на товары для водоснабжения от 3 000 ₽",
 "type": "FIXED",
 "description": "Полезный Маркет Бонус! С ним вы можете сэкономить 300 ₽, когда будете покупать товары для водоснабжения от 3 000 ₽. Кстати, использовать эту скидку можно вместе с другими Маркет Бонусами.",
 "images": {
  "standard": "https://avatars.mds.yandex.net/get-smart_shopping/1546391/8ed3b42b-aef0-4492-8c18-65f33f4a45fe/"
 },
 "status": "ACTIVE",
 "reason": "FOR_USER_ACTION",
 "title": "Скидка 300 ₽",
 "endDate": "2020-03-31T20:59:59.000Z",
 "creationDate": "2020-02-21T04:17:21.000Z",
 "nominal": {
  "value": 300,
  "currency": "RUR"
 },
 "backgroundColor": "#b3b3b3",
 "restrictions": [
  {
   "restrictionType": "CATEGORY",
   "msku": null,
   "categoryId": 16207941
  }
 ]
};

<div>
    <ViewPort width={320} height={300}>
        <Title size='200'> &lt; 375px </Title>
        <div style={{display: 'flex', justifyContent: 'space-around'}}>
            <Coin
                size='100'
                coin={coin}
            />
            <Coin
                size='100'
                coin={coinWithTimer}
            />
        </div>
    </ViewPort>

    <ViewPort width={400} height={300}>
        <Title size='200'> &gt;= 375px </Title>
        <div style={{display: 'flex', justifyContent: 'space-around'}}>
            <Coin
                size='100'
                coin={coin}
            />
            <Coin
                size='100'
                coin={coinWithTimer}
            />
        </div>
    </ViewPort>

</div>
```

#### size '200'
Получение ачивки, тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};
const coinWithTimer = {
 "id": 155866506,
 "subtitle": "на товары для водоснабжения от 3 000 ₽",
 "type": "FIXED",
 "description": "Полезный Маркет Бонус! С ним вы можете сэкономить 300 ₽, когда будете покупать товары для водоснабжения от 3 000 ₽. Кстати, использовать эту скидку можно вместе с другими Маркет Бонусами.",
 "images": {
  "standard": "https://avatars.mds.yandex.net/get-smart_shopping/1546391/8ed3b42b-aef0-4492-8c18-65f33f4a45fe/"
 },
 "status": "ACTIVE",
 "reason": "FOR_USER_ACTION",
 "title": "Скидка 300 ₽",
 "endDate": "2020-03-31T20:59:59.000Z",
 "creationDate": "2020-02-21T04:17:21.000Z",
 "nominal": {
  "value": 300,
  "currency": "RUR"
 },
 "backgroundColor": "#b3b3b3",
 "restrictions": [
  {
   "restrictionType": "CATEGORY",
   "msku": null,
   "categoryId": 16207941
  }
 ]
};

<div>
    <ViewPort width={320} height={400}>
        <Title size='200'> &lt; 375px </Title>
        <div style={{display: 'flex', justifyContent: 'space-around'}}>
            <Coin
                size='200'
                coin={coin}
            />
            <Coin
                size='200'
                coin={coinWithTimer}
            />
        </div>
    </ViewPort>

    <ViewPort width={400} height={400}>
        <Title size='200'> &gt;= 375px </Title>
        <div style={{display: 'flex', justifyContent: 'space-around'}}>
            <Coin
                size='200'
                coin={coin}
            />
            <Coin
                size='200'
                coin={coinWithTimer}
            />
        </div>
    </ViewPort>

</div>
```

#### size '250'
Ачивка, которую можно получить, десктоп.
```jsx
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};

<Coin
    size='250'
    coin={coin}
/>
```

#### size '300'
Полученная ачивка (не выделенная), тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};

<div>
    <ViewPort width={320} height={400}>
        <Title size='200'> &lt; 375px </Title>
        <Coin
            size='300'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={400} height={400}>
        <Title size='200'> &gt;= 375px </Title>
        <Coin
            size='300'
            coin={coin}
        />
    </ViewPort>

</div>
```

#### size '400'
Полученная ачивка (выделенная), тач.
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Title from '@self/root/src/uikit/components/Title';

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};

<div>
    <ViewPort width={320} height={450}>
        <Title size='200'> &lt; 375px </Title>
        <Coin
            size='400'
            coin={coin}
        />
    </ViewPort>

    <ViewPort width={400} height={450}>
        <Title size='200'> &gt;= 375px </Title>
        <Coin
            size='400'
            coin={coin}
        />
    </ViewPort>

</div>
```

#### size '500'
Полученная ачивка, получение ачивки, десктоп.
```jsx
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};

<Coin
    size='500'
    coin={coin}
/>
```

#### fade 'true'
```jsx
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};

<Coin
    size='100'
    coin={coin}
    fade={true}
/>
```

#### isActive 'true'
```jsx
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
    status: 'INACTIVE',
};

<Coin
    size='100'
    coin={coin}
    isActive={true}
/>
```

#### width 'auto'
```jsx
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
};

<div style={{resize: 'horizontal', overflow: 'hidden', padding: 10, width: 200}}>
    <Coin
        size='100'
        coin={coin}
        width='auto'
    />
</div>
```

#### theme 'black'
```jsx
const {$red600} = require('@self/root/src/uikit/palette/colors');

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    backgroundColor: $red600,
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
};

<div style={{background: 'black', padding: 10}} >
    <Coin
        size='100'
        coin={coin}
        theme='black'
    />
</div>
```

#### Монетка с background
```jsx
const {$red600} = require('@self/root/src/uikit/palette/colors');

const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    backgroundColor: $red600,
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/2080eff0-2a8e-4679-926c-032dfb3b29b8'},
};

<Coin
    size='100'
    coin={coin}
/>
```

#### coin.status 'INACTIVE'
Неактивная ачивка
```jsx
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
    status: 'INACTIVE',
};

<Coin
    size='400'
    coin={coin}
/>
```


#### coin.endDate
Ачивка с датой истечения
```jsx
const coin = {
    title: 'Скидка 5%',
    subtitle: 'на любой заказ',
    images: {standard:'https://avatars.mdst.yandex.net/get-smart_shopping/1823/8e001e63-9f43-4b77-8ca9-7c5e8896401c'},
    status: 'INACTIVE',
    endDate: '25-12-2019 03:00:00',
};

<Coin
    size='400'
    coin={coin}
/>
```
