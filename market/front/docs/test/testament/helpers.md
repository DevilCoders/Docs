# Хелперы

В коде маркета уже сформировалось достаточно большое количество хелперов для тестов.
Вот самые полезные из них

## Для инициализации Mirror слоев

### makeMirror

Позволяет инициализировать mirror и слои в платформенных папках
- `market/platform.desktop/helpers/testament/index.js`
- `market/platform.touch/helpers/testament/index.js`

Хелперы поставляют метод `makeMirror()`.
Оба этих хелпера основываются на методе `makeMirror()` из `/src`:
`src/helpers/testament/mirror.js`, а он уже в свою очередь инициализирует слои с дефолтными установками для платформы.

По факту сейчас все тесты на Testament в платформенных папках написаны с его помощью.
В общем виде это выглядит так:

```js
import {makeMirror} from '@self/platform/helpers/testament';

/** @type {Mirror} */
let mirror;
/** @type {JestLayer} */
let jestLayer;
/** @type {MandrelLayer} */
let mandrelLayer;
/** @type {ApiaryLayer} */
let apiaryLayer;
beforeAll(async () => {
    mirror = await makeMirror({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        },
        kadavr: {
            skipLayer: true, // По умолчанию делаем так
        },
    });
    jestLayer = mirror.getLayer('jest');
    mandrelLayer = mirror.getLayer('mandrel');
    apiaryLayer = mirror.getLayer('apiary');
});
```

### makeMirrorTouch и makeMirrorDesktop

Также есть универсальные хелперы, которые можно использовать как в платформе так и в `src/`
Вот тут `@self/root/src/helpers/testament/mirror` написаны хелперы `makeMirrorTouch` и `makeMirrorDesktop`.
В отличие от хелпера `makeMirror` из платформенной папки (в которой мы и так знаем платформу, для которой пишем тест)
`makeMirrorTouch` и `makeMirrorDesktop` инициализируются с конфигами от нужной платформы. В остальном, все также.
Выглядит это так:
```js
import {makeMirrorDesktop} from '@self/root/src/helpers/testament/mirror';

/** @type {Mirror} */
let mirror;
/** @type {JestLayer} */
let jestLayer;
/** @type {MandrelLayer} */
let mandrelLayer;
/** @type {ApiaryLayer} */
let apiaryLayer;

beforeAll(async () => {
    mockLocation();
    mirror = await makeMirrorDesktop({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        },
        kadavr: {
            skipLayer: true,
        },
    });
    jestLayer = mirror.getLayer('jest');
    mandrelLayer = mirror.getLayer('mandrel');
    apiaryLayer = mirror.getLayer('apiary');
});
```

В случае с тачем, все точно также

## Для моков ресурсов

> Все ресурсы мокаются только на стороне бекенда

### Замокать старые ресурсы
`createUnsafeResourceMockImplementation`

```js
await jestLayer.backend.runCode(() => {
    require('@self/project/src/spec/unit/mocks/yandex-market/mandrel/resolver');
    const {unsafeResource} = require('@yandex-market/mandrel/resolver');
    const {createUnsafeResourceMockImplementation} = require('@self/root/src/spec/unit/mocks/resolvers/helpers');
    unsafeResource.mockImplementation(
        createUnsafeResourceMockImplementation({
            'report.getProductsInfo': () => Promise.resolve({...}),
            'report.getTopOffersForProduct': () => Promise.resolve({...}),
        })
    );
}, []);
```

### Замокать новые ресурсы
`mockResource`

```js
await jestLayer.backend.runCode(() => {
        const {cleanUpMocks, saveToCleanUp} = require('@self/root/src/helpers/testament/mockCleanUping');
        const {default: fetchSpecVendorsConfig} = require('@self/root/src/widgets/content/search/__spec__/fixtures/fetchSpecVendorsConfig.fixture');
        
        const {mockResource} = require('@self/root/src/helpers/testament/mock');

        cleanUpMocks('mockNoopBackendFunctionality');

        saveToCleanUp(
            'mockNoopBackendFunctionality',

            mockResource(
                '@self/root/src/resources/s3mds/fetchSpecVendorsConfig',
                'fetchSpecVendorsConfig',
                fetchSpecVendorsConfig
            )                        
        );
    }, []);
```

## Другие полезные хелперы

### Мок mockRouter (buildUrl) в платформе
```js
// в платформе используем так
await jestLayer.runCode(() => {
    const {mockRouter} = require('@self/project/src/helpers/testament/mock');
    mockRouter({
        'external:yandex-passport': () => '//pass-test.yandex.ru',
        'market:index': '//market.yandex.ru',
    });
}, []);
// в src
// использовать src/helpers/testament/mockRouterFabric.js
```

### Моки глобального объекта window
```js
const {
    mockIntersectionObserver,
    mockScrollBy,
    mockLocation,
    mockWindow,
} = require('@self/root/src/helpers/testament/mock');
```
