# Пример теста Hello World!

Рассмотрим написание простейшего теста на примере тестирования простейшего виджета.
Это синтетический пример, на практике виджеты обычно сложнее, но для погружения этого достаточно.
Допустим у нас есть простейший виджет, который ходит за продуктом и рендерит его SLUG. Цель теста:
проверить что SLUG отрендерен верно. Будем мокать поход за продуктом с помощью кадавра.

##Виджет
Итак, наш виджет. Допустим он лежит в `src/widgets/content/BaseWithResolver`
Как и все виджеты, он имеет минимум контроллер, вьюху, индекс, ну, и стили.


`./index.js`
```js

import {Widget} from '@yandex-market/apiary';

import view from './view';
import controller from './controller';

export type Options = {};
export type Data = {
    text: string,
};

export default Widget.describe({
    name: '@MarketNode/Testament/BaseWithResolver',
    view,
    controller,
    directives: {
        asyncController: true,
        static: true
    },
});
```

`./controller.js`
```js

import type {Context} from '@yandex-market/mandrel/context';
import {getSoleParam} from '@yandex-market/mandrel/context';
import {invariant} from '@yandex-market/invariant';

import {selectProductById} from '@self/root/src/entities/product/selectors';
import {resolveProductInfo} from '@self/root/src/resolvers/report';
import {resolveProductInfoParams} from '@self/root/src/resolvers/amp/resolveProductInfoParams';

export default async (ctx: Context) => {
    // ожидаем в урле параметр productId
    const productId = Number(getSoleParam(ctx, 'productId'));
    invariant(Number.isFinite(productId) && productId > 0,
        'Parameter "productId" does not exists or invalid');

    // готовим параметры для похода за продуктом
    const productParams = resolveProductInfoParams(ctx, {productIds: [productId]});

    // идем за продуктом
    const productInfoPromise = resolveProductInfo(ctx, productParams);

    // вытаскиваем продукт
    const product = await productInfoPromise
        .then(({result, collections}) => (result
            ? selectProductById({collections}, result[0])
            : undefined
        ));

    // передаем в data slug продукта
    return {
        data: {
            text: product.slug,
        },
    };
};

```

`./view.js`
```js
import React from 'react';

import {connect} from '@yandex-market/apiary';
import Text from '@self/root/src/uikit/components/Text';

import styles from './styles.styl';

type Props = {
    text: string,
};

const mapStateToProps = ({text}) => ({
    text,
});

// рендерим полученный текст
const View = ({text}: Props) => (
    <span>
        <Text className={styles.root}>{text}</Text>
    </span>
);

export default connect(mapStateToProps)(View);

```

`./styles.styl`
```stylus
.root {
  display: flex;
}
```

## Mocks
Нам потребуются минимальные моки. Для этого создадим папку `__spec__` внутри папки виджета и
положим туда файлик мока с таким содержимым. Мок понадобится в тесте для кадавра
`./__spec__/mocks.js`
```js
export const PRODUCT_ID = 1;
export const OFFER_ID = 2;
export const SLUG = 'telephone';

export const PRODUCT = {
    slug: SLUG,
    type: 'model',
};

export const OFFER = {
    entity: 'offer',
    showUid: OFFER_ID,
};
```

## Тест на Testament
Теперь можно приступать к написанию теста на наш виджет.
Создадим файлик `index.desktop.spec.js` в папке `__spec__`, закинем в него наш
[шаблон](boilerplate.md) и поменяем несколько строк под наши собственные пути

```js
// kadavr helpers
import {
    createProduct,
    mergeState,
    createOfferForProduct,
    createOffer,
} from '@yandex-market/kadavr/mocks/Report/helpers';
// testament mirror
import {makeMirrorDesktop as makeMirror} from '@self/root/src/helpers/testament/mirror.js';
// mocks
import {OFFER, OFFER_ID, PRODUCT, PRODUCT_ID, SLUG} from './mocks';
// widget path
const WIDGET_PATH = '@self/root/src/widgets/content/BaseWithResolver';

/** @type {Mirror} */
let mirror;
/** @type {MandrelLayer} */
let mandrelLayer;
/** @type {ApiaryLayer} */
let apiaryLayer;
/** @type {KadavrLayer} */
let kadavrLayer;

// инициализация контекста
const makeContext = async () => {
    // нужно для работы кадавра
    const cookie = {kadavr_session_id: await kadavrLayer.getSessionId()};

    return mandrelLayer.initContext({
        request: {
            cookie,
            params: {
                // Параметр который ждет контроллер
                productId: PRODUCT_ID,
            },
        },
    });
};

// инициализация кадавра
const setReportState = async () => {
    const offer = createOffer(OFFER);
    const reportState = mergeState([
        createProduct(PRODUCT, PRODUCT_ID),
        createOfferForProduct(offer, PRODUCT_ID, OFFER_ID),
        {
            data: {
                search: {
                    total: 1,
                },
            },
        },
    ]);
    await kadavrLayer.setState('report', reportState);
};

// выполнятся перед всеми тестами
beforeAll(async () => {
    // базовая инициализация с кадавром
    mirror = await makeMirror({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        },
    });
    mandrelLayer = mirror.getLayer('mandrel');
    kadavrLayer = mirror.getLayer('kadavr');
    apiaryLayer = mirror.getLayer('apiary');
});

// выполняется после всех тестов
afterAll(() => {
    mirror.destroy();
});

// сам тест
describe('Простой тест с кадавром', () => {
    test('Должны поймать slug из кадавра', async () => {
        // инициализируем контекст
        await makeContext();
        // инициализируем кадавр
        await setReportState();
        // Маунт виджета через apiaryLayer.
        await apiaryLayer.mountWidget(WIDGET_PATH);
        // проверяем что SLUG из кадавра содержится в рендере
        expect(screen.getByText(SLUG)).toBeInTheDocument();
    });
});
```

Тут мы даже обошлись без моков jestLayer, но с моками на кадавре. Но Вот пример, как можно было сделать без кадавра:

> Премер ниже добавлен только для ознакомления, лучше использовать моки кадавра

```js
// testament mirror
import {makeMirrorDesktop as makeMirror} from '@self/root/src/helpers/testament/mirror.js';
// mocks
import {mockResource, PRODUCT_ID, SLUG} from './mocks';
// widget path
const WIDGET_PATH = '@self/root/src/widgets/content/BaseWithResolver';

/** @type {Mirror} */
let mirror;
/** @type {MandrelLayer} */
let mandrelLayer;
/** @type {ApiaryLayer} */
let apiaryLayer;
/** @type {JestLayer} */
let jestLayer;

// инициализация контекста
const makeContext = async () => {
    // сессия кадавра в куках не нужна
    return mandrelLayer.initContext({
        request: {
            params: {
                // Параметр который ждет контроллер
                productId: PRODUCT_ID,
            },
        },
    });
};

// выполнятся перед всеми тестами
beforeAll(async () => {
    // базовая инициализация с кадавром
    mirror = await makeMirror({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        },
        kadavr: {
            // с этой опцией даже не будем регистрировать слой кадвара
            skipLayer: true,
        },
    });
    mandrelLayer = mirror.getLayer('mandrel');
    jestLayer = mirror.getLayer('jest');
    apiaryLayer = mirror.getLayer('apiary');

    // мокаем ресурс к которому ходит контроллер через резолвер
    // resolveProductInfo
    await jestLayer.backend.runCode(mockResource => {
        jest.doMock('@self/root/src/resources/report', () => ({
            fetchProductInfo: jest.fn().mockResolvedValue(mockResource),
        }));
    }, [mockResource]);

});

// выполняется после всех тестов
afterAll(() => {
    mirror.destroy();
});

// сам тест
describe('Простой тест с кадавром', () => {
    test('Должны поймать slug из кадавра', async () => {
        // инициализируем контекст
        await makeContext();
        // Маунт виджета через apiaryLayer.
        await apiaryLayer.mountWidget(WIDGET_PATH);
        // проверяем что SLUG из кадавра содержится в рендере
        expect(screen.getByText(SLUG)).toBeInTheDocument();
    });
});
```

{% note info %}

Мы не переиспользуем `PageObject`'ы. Они имели смысл в контексте гермионы, но сейчас мы следуем [практикам `testing-library`](../rtl.md) и тестируем интерфейс так, как пользователи взаимодействуют с ним. [Полный список запросов на выбор элементов](https://testing-library.com/docs/queries/about).

{% endnote %}

Мы избавились от кадавра, но добавился новый мок - `mockResource`, который нужно где-то достать :)
В нашем примере он лежит в файлике `./__spec__/mocks.js` и это просто скопипастеный ответ бекенда. Что-то вроде:

```js
...
export const SLUG = 'telephone';
...
export const mockResource = {
    "search": {
        "total": 1,
        "totalOffers": 0,
        "totalFreeOffers": 0,
        "totalOffersBeforeFilters": 0,
        "totalModels": 0,
        "totalPassedAllGlFilters": 0,
        ...
        "results": [{
            "entity": "sku",
            "titles": {
                "raw": "Мягкая игрушка Star Wars Герои GXB23, 20 см, желтый",
                "highlighted": [{"value": "Мягкая игрушка Star Wars Герои GXB23, 20 см, желтый"}]
            },
            "slug": SLUG,
            ...
        }]
    }
}
```



