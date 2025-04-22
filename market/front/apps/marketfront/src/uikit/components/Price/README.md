```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import Text from '@self/root/src/uikit/components/Text';
const InformationPanel = require('@self/root/src/components/InformationPanel').default;
const {buildFormattedPrice} = require('@self/root/src/entities/price');

const store = createStore(() => ({
    collections: {},
}));

const price = {
    currency: 'RUR',
    value: '3389'
};

const example = "<Text theme='error'>-{buildFormattedPrice(price)}</Text>";

<Provider store={store}>
    <div>
        <br/>

        <InformationPanel theme={'normal'} icon='info'>
            <InformationPanel.Title>
                Важно!
            </InformationPanel.Title>
            <InformationPanel.Content>
                <div>
                    Price является частью компонента DiscountPrice, скорее всего вам нужно использовать его.
                    DiscountPrice используется как ценник товара.
                </div>
                <br/>
                <div>
                    Если необходимо вывести не ценник, а просто цену, например как в саммари корзины,
                    тогда используйте <code>buildFormattedPrice</code> (из <code>@self/root/src/entities/price</code>).
                    <br/>
                    Например, вот так
                    <br/>
                    <code>{example}</code>
                    <br/>
                    <Text theme='error'>
                        -{buildFormattedPrice(price)}
                    </Text>
                </div>
            </InformationPanel.Content>
        </InformationPanel>

        <br/>
    </div>
</Provider>

```

### Песочница
```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground component={Price} />
</Provider>
```

### Примеры

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <div>

        <h3>Все размеры с дефолтной темой</h3>
        <hr />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
        />

        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='s'
        />

        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='m'
        />

        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='l'
        />

        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='xl'
        />

        <h3>Все размеры с темой accent</h3>
        <hr />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='accent'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='accent'
            size='s'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='accent'
            size='m'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='accent'
            size='l'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='accent'
            size='xl'
        />
        <br />
        <br />

        <h3>Все размеры с темой lineThrough</h3>
        <hr />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='lineThrough'
        />

        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='s'
            theme='lineThrough'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='m'
            theme='lineThrough'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='l'
            theme='lineThrough'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='xl'
            theme='lineThrough'
        />
        <br />
        <br />


        <h3>Все размеры с темой purple</h3>
        <hr />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='purple'
        />

        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='s'
            theme='purple'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='m'
            theme='purple'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='l'
            theme='purple'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='xl'
            theme='purple'
        />
        <br />
        <br />

        <h3>Все размеры с темой lineThroughPurple</h3>
        <hr />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            theme='lineThroughPurple'
        />

        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='s'
            theme='lineThroughPurple'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='m'
            theme='lineThroughPurple'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='l'
            theme='lineThroughPurple'
        />
        <br />
        <br />

        <Price
            price={{
                currency: 'RUR',
                value: '3389'
            }}
            size='xl'
            theme='lineThroughPurple'
        />
        <br />
        <br />

    </div>
</Provider>
```
