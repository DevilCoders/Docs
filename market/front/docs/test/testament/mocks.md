# Примеры моков

## Моки бекенда при помощи KadavrLayer (рекомендовано)
### Пример мока для Cataloger

```js
// Пример 1

await kadavrLayer.setState('Cataloger.stat', {
    baseAssemblyEnd: '2022-04-08 11:20:35',
    baseAssemblyStart: '2022-04-08 10:15:43.591472',
    baseId: '20220408_1015',
    baseReleaseComplete: '2022-04-08 11:26',
    offersCount: '1115506',
    shopCount: '237',
});

// Пример 2

await kadavrLayer.setState('Cataloger.tree', navigationTree);
```

### Пример мока для Report

```js
// Хелперы для кадавра тут

import {
    createOffer,
    createProduct,
    createOfferForProduct,
    mergeState,
} from '@yandex-market/kadavr/mocks/Report/helpers';

// Пример 1

const reportProduct = createProduct({
    type: 'model',
    categories: [{
        id: 123,
    }],
    slug: 'random-fake-slug',
    deletedId: null,
}, reviewProductId);

await kadavrLayer.setState('report', reportProduct);

// Пример 2

const reportProduct = createProduct({
    type: 'model',
    categories: [{
        id: 123,
    }],
    slug: reviewProductSlug,
    deletedId: null,
}, reviewProductId);

const offerForProduct = createOfferForProduct({
    cpa: 'real',
}, reviewProductId, offerForReviewProductId);

await kadavrLayer.setState('report', mergeState([
    reportProduct,
    offerForProduct,
]));
```

## Мок резолвера

> ⚠️ Лучше мокать бекенд через кадавра, но просто для информации, мок резолверов и ресурсов тоже доступен
> Резолверы и ресурсы мокаются только на строне бекенда

```js
// Пример 1 (используя аргументы)
await jestLayer.backend.runCode((resolveProductInfo, mock) => {
    jest.doMock(
        resolveProductInfo,
        () => jest.fn().mockResolvedValue(mock)
    );
}, [
    require.resolve('@self/root/src/resolvers/report/resolveProductInfo'),
    mock,
]);
// Пример 2 (с __esModule)
await jestLayer.backend.doMock(
    require.resolve('@self/platform/resolvers/shops/info'),
    () => ({
        __esModule: true,
        resolveSupplierInfo: () => Promise.resolve({
            entities: {
                supplierInfo: {},
            },
            result: [],
        }),
    })
);

// Пример 3 (простой spyOn)
await jestLayer.backend.runCode(() => {
    jest.spyOn(require('@yandex-market/mandrel/resolvers/page'), 'resolvePageIdSync')
        .mockReturnValue('market:catalog');
}, []);

// Пример 4 (spyOn с моком переданным через аргумент)
// если мок заркварен где то выше по уровню, то внутри runCode его не увидим! Поэтому передаем через аргумент
// можно зарекварить мок внутри runCode, тут вкусовщина/целесообразность.
await jestLayer.backend.runCode((mock) => {
    jest.spyOn(require('@self/root/src/resolvers/user'), 'resolveSessionSync').mockReturnValue(mock);
}, [someMock]);
```

### Где брать данные для мока (только для мока ресурсов)

Вы можете запустить любой кадавр-мок и замокать любой резолвер или ресурс полученными от мока данными.

```ts
import TestMock from '@yandex-market/kadavr/mocks/SomeMock'; // самый обычный кадавровый мок
import InMemoryState from '@yandex-market/kadavr/dist/state/inMemory'; // стейт для мока
import {makeRequest, makeResponse} from '@yandex-market/kadavr/dist/mockExecutor'; // хелперы для запуска мока

// мокаем резолвер или ресурс
await jestLayer.backend.doMock('path/to/someResource', async (ctx, params) => {
    const state = new InMemoryState(); // создаем стейт для мока (можно передать кастомный initial state)
    const mock = new TestMock(state); // создаем мок
    await mock.init(); // ждем инициализации мока
    return mock.action(makeRequest(params), makeResponse()); // вызываем метод мока и возвращаем результат
});
```

## Мок платформы
```js
jest.doMock('@self/root/src/entities/platform/utils', () => ({
    getPlatform: () => 'desktop',
    isApiPlatform: () => false,
}));
```

## Мок файла под платформу
```js
await jestLayer.runCode(() => {
    jest.doMock(
        '@self/root/src/widgets/CheckoutAgreementNote/View',
        () => jest.requireActual('@self/root/src/widgets/CheckoutAgreementNote/View/index.touch.js')
    );
}, []);
```

## Мок селекторов

> ⚠️ Скорее всего, если вам хочется замокать селектор, то вы делаете что-то не так

```js
jest.spyOn(
    require('@self/root/src/selectors/checkout/purchase'),
    'selectFullDataForActualization'
).mockReturnValue(fullDataForActualizationWithEmit);
```

## Эксперименты
```js
jest.spyOn(require('@self/root/src/resolvers/experimentFlags'), 'resolveExperimentFlagsSync').mockReturnValue({
    result: [],
    collections: {
        experimentFlag: {},
    },
});
```

## Мок виджета (если есть слот, который хотим проигнорировать)

```js
await jestLayer.doMock(
    require.resolve('@self/platform/widgets/content/FinancialProduct'),
    () => ({create: () => Promise.resolve(null)})
);
```

## Мок Гарсона

```js
return mirror.getLayer('jest').runCode(() => {
    require('@self/project/src/legacy/modules/DataCollector').register(
        require('@self/platform/app/modules/DataCollector/garsons'),
        require('@self/platform/app/modules/DataCollector/completers')
    );
}, []);
```

### Мок роутера

```js

// Пример 1 (топором)
await jestLayer.doMock(
    require.resolve('@self/project/src/utils/router'),
    () => ({buildURL: () => ''})
);

// Пример 2 (проект/платформа)
await jestLayer.runCode(() => {
    const {mockRouter} = require('@self/project/src/helpers/testament/mock');
    mockRouter();
}, []);

// Пример 3 (src)
jestLayer.runCode(() => {
    const {mockRouterFabric} = require('@self/root/src/helpers/testament/mock');
    mockRouterFabric()({
        'touch:catalog': ({slug, nid}) => `/catalog--${slug}/${nid}`,
        'touch:list': ({slug, nid}) => `/catalog--${slug}/${nid}/list`,
        'touch:purchased': '/my/purchased',
    });
}, []);
```

### Диспатч экшена

```js
import {screen} from '@testing-library/dom';
import SharedActionEmitter from '@yandex-market/apiary/client/sharedActionEmitter';
import {BOUND_PHONE_DIALOG_OPEN} from '@self/platform/actions/boundPhoneDialog';

...

describe('Диалог подтверждения телефона для домена .by.', () => {
    beforeEach(async () => {
        await mandrelLayer.initContext();
    });
    test('Отображается', async () => {
        await apiaryLayer.mountWidget(widgetPath);
        const globalSharedActionEmitter = new SharedActionEmitter();
        globalSharedActionEmitter.dispatch({
            type: BOUND_PHONE_DIALOG_OPEN,
        });
        return expect(screen.findByText('Привязать номер')).toBeTruthy();
    });
});
```
