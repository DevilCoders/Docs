### Сниппет



```jsx
const {map, get} = require('lodash/fp');
const classNames = require('classnames');
const DropdownNative = require('@self/root/src/uikit/components/DropdownNative').default;
const ScrollBox = require('@self/root/src/components/ScrollBox');
const styles = require('./Readme.styles.styl');
const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;

const pack = {
    partPrice: {
      value: '65780',
      currency: 'RUR'
    },
    partUnit: 'шт',
    partSize: 2,
    packSize: 10,
};

const reasonsToBuy = [
    {
        id: "customers_choice",
        value: 0.92,
    },
    {
        id: "best_by_factor",
        factor_name: "Объем памяти",
        value: 0.8,
    },
    {
        id: "compatible_with_alisa",
    },
    {
        id: "alisa_lives_here",
    }
];

initialState = {
    count: 4,
    options: [4, 6, 8, 10, 12].map(value => ({text: value, value})),

    theme: 'uno',
    themes: [
        {
            value: 'uno',
            text: '1. Uno',
        },
        {
            value: 'dos',
            text: '2. Dos',
        },
        {
            value: 'tres',
            text: '3. Tres',
        },
        {
            value: 'cuatro',
            text: '4. Cuatro',
        },
        {
            value: 'cinco',
            text: '5. Cinco',
        },
        {
            value: 'seis',
            text: '6. Seis',
        },
        {
            value: 'siete',
            text: '7. Siete',
        },
        {
            value: 'ocho',
            text: '8. Ocho',
        },
        {
            value: 'nueve',
            text: '9. Nueve',
        },
        {
            value: 'diez',
            text: '10. Diez',
        },
        {
            value: 'once',
            text: '11. Once',
        },
        {
            value: 'doce',
            text: '12. Diez',
        },
        {
            value: 'trece',
            text: '13. Trece',
        },
        {
            value: 'catorce',
            text: '14. catorce',
        },
        {
            value: 'quince',
            text: '15. Quince',
        },
        {
            value: 'treinta',
            text: '30. treinta',
        },
    ],
    snippets: [
        {
            picture: {"entity": "picture", "original": {"containerWidth": 444, "containerHeight": 701, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/orig", "width": 444, "height": 701 }, "thumbnails": [{"containerWidth": 50, "containerHeight": 50, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/50x50", "width": 31, "height": 50 }, {"containerWidth": 55, "containerHeight": 70, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/55x70", "width": 44, "height": 70 }, {"containerWidth": 60, "containerHeight": 80, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/60x80", "width": 50, "height": 80 }, {"containerWidth": 74, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/74x100", "width": 63, "height": 100 }, {"containerWidth": 75, "containerHeight": 75, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/75x75", "width": 47, "height": 75 }, {"containerWidth": 90, "containerHeight": 120, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/90x120", "width": 76, "height": 120 }, {"containerWidth": 100, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/100x100", "width": 63, "height": 100 }, {"containerWidth": 120, "containerHeight": 160, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/120x160", "width": 101, "height": 160 }, {"containerWidth": 150, "containerHeight": 150, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/150x150", "width": 95, "height": 150 }, {"containerWidth": 180, "containerHeight": 240, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/180x240", "width": 152, "height": 240 }, {"containerWidth": 190, "containerHeight": 250, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/190x250", "width": 158, "height": 250 }, {"containerWidth": 200, "containerHeight": 200, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/200x200", "width": 126, "height": 200 }, {"containerWidth": 240, "containerHeight": 320, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/240x320", "width": 202, "height": 320 }, {"containerWidth": 300, "containerHeight": 300, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/300x300", "width": 190, "height": 300 }, {"containerWidth": 300, "containerHeight": 400, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/300x400", "width": 253, "height": 400 }, {"containerWidth": 600, "containerHeight": 600, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id17762228101150277.jpeg/600x600", "width": 380, "height": 600 } ] },
            title: "Название товара",
            priceDescription: "Цена от Сбербанка",
            rating: 5,
            opinions: 22,
            variants: 2,
            price: {
                currentPrice: {
                    value: 65780,
                    currency: 'RUR'
                },
                oldPrice: {
                    value: 89456,
                    currency: 'RUR'
                },
                percent: 25
            },
            pack: pack,
            reasonsToBuy,
            monthlyPayment: {
                value: 10000,
                currency: 'RUR'
            },
        },
        {
            picture: {"entity": "picture", "original": {"containerWidth": 308, "containerHeight": 596, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/orig", "width": 308, "height": 596 }, "thumbnails": [{"containerWidth": 50, "containerHeight": 50, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/50x50", "width": 25, "height": 50 }, {"containerWidth": 55, "containerHeight": 70, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/55x70", "width": 36, "height": 70 }, {"containerWidth": 60, "containerHeight": 80, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/60x80", "width": 41, "height": 80 }, {"containerWidth": 74, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/74x100", "width": 51, "height": 100 }, {"containerWidth": 75, "containerHeight": 75, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/75x75", "width": 38, "height": 75 }, {"containerWidth": 90, "containerHeight": 120, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/90x120", "width": 62, "height": 120 }, {"containerWidth": 100, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/100x100", "width": 51, "height": 100 }, {"containerWidth": 120, "containerHeight": 160, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/120x160", "width": 82, "height": 160 }, {"containerWidth": 150, "containerHeight": 150, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/150x150", "width": 77, "height": 150 }, {"containerWidth": 180, "containerHeight": 240, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/180x240", "width": 124, "height": 240 }, {"containerWidth": 190, "containerHeight": 250, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/190x250", "width": 129, "height": 250 }, {"containerWidth": 200, "containerHeight": 200, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/200x200", "width": 103, "height": 200 }, {"containerWidth": 240, "containerHeight": 320, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/240x320", "width": 165, "height": 320 }, {"containerWidth": 300, "containerHeight": 300, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/300x300", "width": 155, "height": 300 }, {"containerWidth": 300, "containerHeight": 400, "url": "//avatars.mds.yandex.net/get-mpic/364668/img_id4800288872801570040/300x400", "width": 206, "height": 400 } ] },
            title: "Смартфон LG K8 (2017) X240 индиго",
            rating: 4,
            opinions: 7,
            price: {
                currentPrice: {
                    value: 1200,
                    currency: 'RUR'
                },
                oldPrice: {
                    value: 1234,
                    currency: 'RUR'
                }
            },
        },
        {
            picture: {"entity": "picture", "original": {"containerWidth": 701, "containerHeight": 543, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/orig", "width": 701, "height": 543 }, "thumbnails": [{"containerWidth": 50, "containerHeight": 50, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/50x50", "width": 50, "height": 38 }, {"containerWidth": 55, "containerHeight": 70, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/55x70", "width": 55, "height": 42 }, {"containerWidth": 60, "containerHeight": 80, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/60x80", "width": 60, "height": 46 }, {"containerWidth": 74, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/74x100", "width": 74, "height": 57 }, {"containerWidth": 75, "containerHeight": 75, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/75x75", "width": 75, "height": 58 }, {"containerWidth": 90, "containerHeight": 120, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/90x120", "width": 90, "height": 69 }, {"containerWidth": 100, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/100x100", "width": 100, "height": 77 }, {"containerWidth": 120, "containerHeight": 160, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/120x160", "width": 120, "height": 92 }, {"containerWidth": 150, "containerHeight": 150, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/150x150", "width": 150, "height": 116 }, {"containerWidth": 180, "containerHeight": 240, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/180x240", "width": 180, "height": 139 }, {"containerWidth": 190, "containerHeight": 250, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/190x250", "width": 190, "height": 147 }, {"containerWidth": 200, "containerHeight": 200, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/200x200", "width": 200, "height": 154 }, {"containerWidth": 240, "containerHeight": 320, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/240x320", "width": 240, "height": 185 }, {"containerWidth": 300, "containerHeight": 300, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/300x300", "width": 300, "height": 232 }, {"containerWidth": 300, "containerHeight": 400, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/300x400", "width": 300, "height": 232 }, {"containerWidth": 600, "containerHeight": 600, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/600x600", "width": 600, "height": 464 }, {"containerWidth": 600, "containerHeight": 800, "url": "//avatars.mds.yandex.net/get-mpic/1244413/img_id6618365739037772765.jpeg/600x800", "width": 600, "height": 464 } ] },
            title: "Зеркальный фотоаппарат Canon EOS 750D Kit черный EF-S 18-55mm f/3.5-5.6 IS STM",
            rating: 24,
            opinions: 0,
            price: {
                currentPrice: {
                    value: 1200,
                    currency: 'RUR'
                },
            },
        },
        {
            picture: {"entity": "picture", "original": {"containerWidth": 316, "containerHeight": 604, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/orig", "width": 316, "height": 604 }, "thumbnails": [{"containerWidth": 50, "containerHeight": 50, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/50x50", "width": 26, "height": 50 }, {"containerWidth": 55, "containerHeight": 70, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/55x70", "width": 36, "height": 70 }, {"containerWidth": 60, "containerHeight": 80, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/60x80", "width": 41, "height": 80 }, {"containerWidth": 74, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/74x100", "width": 52, "height": 100 }, {"containerWidth": 75, "containerHeight": 75, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/75x75", "width": 39, "height": 75 }, {"containerWidth": 90, "containerHeight": 120, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/90x120", "width": 62, "height": 120 }, {"containerWidth": 100, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/100x100", "width": 52, "height": 100 }, {"containerWidth": 120, "containerHeight": 160, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/120x160", "width": 83, "height": 160 }, {"containerWidth": 150, "containerHeight": 150, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/150x150", "width": 78, "height": 150 }, {"containerWidth": 180, "containerHeight": 240, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/180x240", "width": 125, "height": 240 }, {"containerWidth": 190, "containerHeight": 250, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/190x250", "width": 130, "height": 250 }, {"containerWidth": 200, "containerHeight": 200, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/200x200", "width": 104, "height": 200 }, {"containerWidth": 240, "containerHeight": 320, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/240x320", "width": 167, "height": 320 }, {"containerWidth": 300, "containerHeight": 300, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/300x300", "width": 156, "height": 300 }, {"containerWidth": 300, "containerHeight": 400, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/300x400", "width": 209, "height": 400 }, {"containerWidth": 600, "containerHeight": 600, "url": "//avatars.mds.yandex.net/get-mpic/932277/img_id1900985866524569431.jpeg/600x600", "width": 313, "height": 600 } ] },
            title: "Смартфон Samsung Galaxy J2 Prime SM-G532F серебристый",
            rating: 3,
            opinions: 24,
            price: {
                currentPrice: {
                },
            },
        },
    ],
};

const store = createStore(() => ({collections: {}}));

const SnippetWrapper = props => (
    <Provider store={store}>
        <Snippet {...props} />
    </Provider>
);

const getSnippetByIndex = (index) => state.snippets.find((item, key) => index % state.snippets.length === key);
const getThemeValue = () => state.theme;
const setTheme = (theme) => setState({theme});

const getCountSnippets = () => Number(state.count);
const setCountSnippets = (count) => setState({count});

<div className={styles.root} style={{position: 'relative'}}>
    <h3>Выберите тему:</h3>
    <DropdownNative
        options={state.themes}
        onChange={({currentTarget: {value}}) => setTheme(value)}
        value={getThemeValue()}
    />

    <h3>Сниппеты</h3>
    <div className={classNames(styles.wrapper, {[styles[state.theme]]: true})}>
        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showRating
                showTitle
                showReasons
                showVariants
                showPack
                showMonthlyPayment
                showCustomersChoice
                showBestFactor
                showAlisaReasons
            />
        </div>
        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showRating
                showTitle
                showReasons
                showVariants
                showPack
                showMonthlyPayment
            />
        </div>
        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showRating
                showTitle
                showReasons
                showVariants
                showPack
                showCustomersChoice
                showBestFactor
            />
        </div>
        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showRating
                showTitle
                showReasons
            />
        </div>
        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showRating
                showTitle
            />
        </div>
        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showTitle
            />
        </div>

        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
            />
        </div>

        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
            />
        </div>

        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showPriceDescription
                showMonthlyPayment
                showRating
            />
        </div>

        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showPriceDescription
                showRating
                showTitle
                showReasons
            />
        </div>

        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showPriceDescription
                showTitle
            />
        </div>

        <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(0)}
                theme={getThemeValue()}
                showPrice
                showPriceDescription
                showTitle
            />
        </div>

         <div className={styles.item}>
            <SnippetWrapper
                {...getSnippetByIndex(1)}
                theme={getThemeValue()}
                showPrice
                showPriceDescription
                showTitle
            />
        </div>
    </div>

    <h3>Пример сетки</h3>
    <DropdownNative
        options={state.options}
        onChange={({currentTarget: {value}}) => setCountSnippets(value)}
        value={getCountSnippets()}
    />

    <div className={classNames(styles.wrapper, {[styles[state.theme]]: true})}>
        {Array(getCountSnippets()).fill(0).map((val, index) =>
            <div className={styles.item}>
                <SnippetWrapper
                    key={index}
                    {...getSnippetByIndex(index)}
                    theme={getThemeValue()}
                    showPrice
                    showRating
                    showTitle
                />
            </div>
        )}
    </div>
    <br/>


</div>
```
