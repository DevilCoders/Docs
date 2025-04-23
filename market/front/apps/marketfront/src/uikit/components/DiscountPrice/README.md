### Блок с ценой Купона

#### Пример

### Песочница
```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import Text from '@self/root/src/uikit/components/Text';
import Wrapper from '@self/root/src/components/WidgetWrapper';
import Title from '@self/root/src/uikit/components/Title';

const store = createStore(() => ({
    collections: {},
}));

const Wrap = ({children, title}) => (
    <Wrapper
        title={{
            size: '100',
            text: title,
            theme: 'muted',
            indent: '3'
        }}
        margins={{
            top: '5'
        }}
    >
        {children}
    </Wrapper>
);
<Provider store={store}>
    <Helper.Playground
        component={DiscountPrice}
        example={props => {
            return (
                <div>
                    <Wrap title="Без монет">
                        <DiscountPrice {...props} />
                    </Wrap>
                    <Wrap title="С промо">
                        <DiscountPrice {...props} promo="cart-discount" />
                    </Wrap>
                </div>
            )
        }}
    />
</Provider>
```


```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    currentPrice: 5000,
    oldPrice: 10000,
    size: 'xl',
};

const withoutOldPrice = {
    currentPrice: {
        value: '29989',
        currency: 'RUR'
    },
    promo: 'cart-discount'
};

const withAbsoluteDiscount = {
    currentPrice: {
        value: '29989',
        currency: 'RUR'
    },
    oldPrice: {
        value: '39989',
        currency: 'RUR'
    },
    oldDiscountPrice: {
        value: '34989',
        currency: 'RUR'
    },
    absolute: {
        value: '10000',
        currency: 'RUR'
    }
};

const onCurrentPriceChange = evt => {
    setState({
        currentPrice: evt.target.value
    });
};

const onOldPriceChange = evt => {
    setState({
        oldPrice: evt.target.value
    });
};

const sizes = ['xl', 'l', 'm', 's', 'xs'];

const renderPrices = (props, column = false) => {
    return sizes.map(size =>
        <div style={{marginBottom: 15}} key={size}>
            <DiscountPrice {...props} size={size} />
        </div>
    );
};


<Provider store={store}>
    <div>
        <h3>Все размеры со старой ценой</h3>
        <hr />

        <table>
            <thead>
                <tr>
                    <td>Новая цена</td>
                    <td>Старая цена</td>
                </tr>
            </thead>
            <thead>
                <tr>
                    <td>
                        <input type="number" onInput={onCurrentPriceChange} value={state.currentPrice} />
                    </td>
                    <td>
                        <input type="number" onInput={onOldPriceChange} value={state.oldPrice} />
                    </td>
                </tr>
            </thead>
        </table>

        <br />

        {renderPrices({
            price: {
                currentPrice: {
                    value: state.currentPrice,
                    currency: 'RUR'
                },
                oldPrice: {
                    value: state.oldPrice,
                    currency: 'RUR'
                }
            },
            column: false
        })}

        <h3>Все размеры со старой ценой в колонку</h3>
        <hr />

        {renderPrices({
            price: {
                currentPrice: {
                    value: state.currentPrice,
                    currency: 'RUR'
                },
                oldPrice: {
                    value: state.oldPrice,
                    currency: 'RUR'
                }
            },
            column: true
        })}

        <h3>Все размеры при отсутствии старой цены</h3>
        <hr />

        {renderPrices({price: withoutOldPrice})}

        <h3>Все размеры с абсолютной скидкой</h3>

        <hr />

        {renderPrices({
            price: withAbsoluteDiscount,
            withAbsoluteDiscount: true
        })}

        <h3>Все размеры с абсолютной скидкой в колонку</h3>

        <hr />

        {renderPrices({
            price: withAbsoluteDiscount,
            withAbsoluteDiscount: true,
            column: true,
        })}
    </div>
</Provider>
```
