### Компонент "фичеренного" товара

С помощью этого компонента можно дать особенную картинку
и особенное описание для товара

```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const {littlePicture, bigPicture} = require('./stubThumbs');

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground
        component={PromoFeatured}
        defaultValues={{
            title: helper.generateText({words: 20})
        }}
        props={{
            picture: {
                type: 'enum',
                required: true,
                defaultValue: littlePicture,
                values: [littlePicture, bigPicture],
            },
            subtitles: {
                type: 'enum',
                required: false,
                values: [[
                    helper.generateText({words: 3}),
                    helper.generateText({words: 2})
                ]]
            }
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

const {littlePicture, bigPicture} = require('./stubThumbs');
const {Grid, Container, Column} = require('@self/root/src/uikit/components/Layout').default;
const currentPrice = 1234;
const oldPrice = 6578;
const price = {
    currentPrice: {
        value: currentPrice,
        currency: 'RUR',
    },
    oldPrice: {
        value: oldPrice,
        currency: 'RUR',
    },
    percent: 100 - Math.round(currentPrice/oldPrice * 100)
};

const props = {
    price,
    title: 'Кастрюля Rondell жёлтая, 2 литра с крышкой',
    subtitles: [
        'Объём: 2 литра',
        'Крышка: стеклянная'
    ],
};

const longTitleProps =
{
    ...props,
    title: 'Длинное название строк на 5. Например, название видеокарты, с кучей параметров, и характерестик, таких как: тип видеопамяти, объем видеопамяти, поколение, количество занимаемых слотов, названия используемых портов, производитель, изобретатель и многое много многое другое'
};

<Provider store={store}>
    <div>
        <h3>Размер `l`</h3>
        <Grid size={24}>
            <h4> Тема `default` </h4>
            <Column size={9}>
                <PromoFeatured picture={littlePicture} {...props} pageId='#' />
            </Column>
            <Column size={9}>
                <PromoFeatured picture={littlePicture} type='default' {...longTitleProps} pageId='#' />
            </Column>
        </Grid>
        <br />
        <Grid size={24}>
            <h4> Тема `overlay` </h4>
            <Column size={9}>
                <PromoFeatured picture={littlePicture} type='overlay' {...props} subtitles={null} pageId='#' />
            </Column>
        </Grid>

        <hr />
        <h3>Размер `xxl`</h3>
        <Grid size={24}>
            <h4> Тема `default` </h4>
            <Column size={12}>
                <PromoFeatured picture={littlePicture} size='xxl' {...props} title="Короткое название" pageId='#' />
            </Column>
            <Column size={12}>
                <PromoFeatured picture={littlePicture} size='xxl' type='default' {...longTitleProps} pageId='#' />
            </Column>
        </Grid>
        <br />
        <Grid size={24}>
            <h4> Тема `overlay` </h4>
            <Column size={24}>
                <PromoFeatured picture={bigPicture} size='xxl' type='overlay' {...{...longTitleProps, subtitles: null}} pageId='#' />
            </Column>
        </Grid>
    </div>
</Provider>

```
