# Market Resource Sugar 🍭

*(Декларативные ресурсы)*

Содержит набор хелперов, предназначенных для облегчения процесса создания ресурсов:
- Значительно сокращает колличество кода для написания ресурса
- Позволяет наследовать конфиги, общие для нескольких методов ресурсов
- Наследовать конфиги можно несколько раз, от общего к частному
- Предоставляет возможность полного или частичного фолбека к базовым методам ресурса


Доступные хелперы:
- [buildQueryParams](./lib/helpers/buildQueryParams.js) - Используется для вычисления query параметров при наследовании конфигов
- [createResourceFactory](./lib/resource/createResourceFactory.js) - Возвращает фабричную ф-ию для создания объекта ресурса
- [inheritResourceConfigs](./lib/resource/inheritResourceConfigs.js)  - Для каждого из конфигов устанавливает значения по умолчанию


Примеры использования:
- Ресурсы [MBI](https://github.yandex-team.ru/market/partnernode/tree/master/app/resource/mbiPayment)
- Ресурсы [Checkouter](https://github.yandex-team.ru/market/partnernode/tree/master/app/resource/checkouter)
- Ресурсы [Report](https://github.yandex-team.ru/market/partnernode/tree/master/app/resource/report)


## Конфигурация создаваемого ресурса (ResourceConfig)
```js
// @flow
type ResourceConfigFields = {...}
type ResourceConfigMerger = (baseConfig: ?ResourceConfigFields) => ResourceConfigFields
type ResourceConfig = ResourceConfigFields|ResourceConfigMerger
```

```js
// Полный набор параметров декларации
module.exports = {
    cfg: {
        // logId умеет устанвливать сам ресурс, поэтому нигде его не указываем
        // https://github.yandex-team.ru/nodules/resource/blob/master/lib/resource.js#L197
        timeout: 10000,
        maxRetries: 1,
        dataType: 'json',
        agent: {
            name: 'mbiPayment',
            maxSockets: 500,
        },
        statusFilter(code) {
            return {
                accept: [200, 201, 400, 403, 404].indexOf(code) !== -1,
                isRetryAllowed: code > 499,
            };
        },
    },
    // кастомная предобработка path, предполагается использование на бозовом конфиге,
    // для получение path из configs/current/node.js
    getPath(path, ctx) {
        return ctx.cfg.path ? `/${ctx.cfg.path}/${path}` : path;
    },
    path: '/getSomeData',
    // path: params => `/orders/${params.orderId}`,

    method: 'GET',
    // method: params => (params.action === 'create' ? 'POST' : 'PUT'),

    body: {
        static: 'content',
    },
    // body: params => {data: params.data},

    bodyEncoding: 'multipart',
    // bodyEncoding: params => params.encoding,

    headers: {
        Accept: 'application/json',
    },
    // headers: params => ({Accept: (params.format === 'json' ? 'application/json' : 'text/html')}),

    // Для большинства кейсов хватает указать constraints объектом, ключами которого будет
    // параметры переданные в ресурс, если указать функцией, то она должна вернуть подобный объект
    constraints: {
        uid: {
           presence: true,
        },
    },
    // constraints: params => ({uid: {presence: params.group === 'manager'}}),

    // Ключами указываем то, что будем отправлять в бекенд, значениями из какого параметра переданного
    // в ресурс получить значение, либо можно задать функцией, которая примает параметры переданные в ресурс
    query: {
        _user_id: 'uid',
        _remote_ip: 'clientIp',
        euid: 'euid',
        format: () => 'json', // стаб значения
        page: params => params.page || 0, // установка дефолтного значения
        sizes: params => `${params.width}x${params.height}`,
    },

    // Все, что угодно. Содержимое будет добавлено в корень, рядом с query.
    // Преобразуется по тем же правилам что и method/body/headers,
    // то есть или значение, или функция от пропсов
    customProps: {
        foo: 'bar',
        baz: params => ({quux: params.foobar}),
    }

    // Может указываться у каждого отдельного метода ресурса
    processHandler,

    // Может указываться у каждого отдельного метода ресурса, вызывается в контексте ресурса
    // должна бросить исключение
    processErrorHandler,
    // Может указываться у каждого отдельного метода ресурса, проверяет наличие ошибок в ответе ресурса
    containsError,
    // Получает данные ошибки из ответа ресурса
    getErrorData,

    // Фолбеки которые полностью переопределяют функции созданные хелперами
    process,
    action,
    prepare,
    error,
}
```

## Наследование конфигураций - inheritResourceConfigs
```js
// @flow
type InheritResourceConfigs = (baseConfig: ResourceConfig, resourceConfigs: {[method: string]: ResourceConfig}) => {[method: string]: ResourceConfigMerger}
```

```js
// a.js
const {inheritResourceConfigs} = require('@yandex-market/resource-sugar');

const mapAlerts = ([{unreadMessagesCount}]) => ({unreadMessagesCount});

// {ResourceConfig} getAlerts
const getAlerts = ({processHandler}) => ({
    path: '/getAlerts',
    processHandler: _.flow([processHandler, mapAlerts]),
});

// {ResourceConfig} getClientIds
const getClientIds = {
    path: '/getClientIds',
};

// {ResourceConfigs}
const resourceConfigs = inheritResourceConfigs({
    constraints: {
        uid: CONSTRAINTS.UID,
    },
}, {
    getAlerts,
    getClientIds,
});
```

В результате работы `inheritResourceConfigs` получится коллекция конфигов ресурсов ожидающая дефолтых значений.

```js
// {ResourceConfigs}
const resourceConfigs = {
    getAlerts: defaults => deepMerge(deepMerge(defaults, clientDefaults), getAlerts(deepMerge(defaults, clientDefaults))),
    getClientIds: defaults => deepMerge(deepMerge(defaults, clientDefaults), getClientIds),
}
```

Так же `inheritResourceConfigs` может принимать первым аргументом фунцию, которая будет ожидать конфиг предыдущего
уровня. Результат работы этой функции будет смержен конфигом предыдущего уровня (который передали первым параметром).
Немного переделав `mapAlerts`, в результате композиций функций получим такой же результат `processHandler`.

```diff
--- a.js
+++ b.js
@@ -1,4 +1,4 @@
-const mapAlerts = ([{unreadMessagesCount}]) => ({unreadMessagesCount});
+const mapAlerts = ({unreadMessagesCount}) => ({unreadMessagesCount});
```

```js
// b.js
const {inheritResourceConfigs} = require('@yandex-market/resource-sugar');

const mapAlerts = ({unreadMessagesCount}) => ({unreadMessagesCount});

// {ResourceConfig} getAlerts
const getAlerts = ({processHandler}) => ({
    path: '/getAlerts',
    processHandler: _.flow([processHandler, mapAlerts]),
});

// {ResourceConfigs}
const resourceConfigs = inheritResourceConfigs(({processHandler})=> ({
    constraints: {
        uid: CONSTRAINTS.UID,
    },
    processHandler: _.flow([processHandler, ([obj]) => obj]),
}), {
    getAlerts,
    getClientIds,
});
```

## Создание фабрики ресурсов - createResourceFactory(Resource: Resource): Function
```js
// app/resource/helpers/createResource.js
const Resource = require('@yandex-market/mandrel/resource');
const {createResourceFactory} = require('@yandex-market/resource-sugar');

module.exports = createResourceFactory(Resource);
```

## Создание новых ресурсов
```js
// app/resource/mbiPayment
const createResource = require('../../helpers/createResource');

const defaultConfig = require('./config');

module.exports = createResource(defaultConfig, [
    // Сгруппированные по смыслу конфиги для методов ресурсов
    ...
    require('./campaign'), // mbiPayment.getCPAState, mbiPayment.getCampaignAdmins ...
    require('./tax-settings'), // mbiPayment.getTaxSettings, mbiPayment.setTaxSettings ...
    require('./delivery'), // mbiPayment.getDeliverySettingsSummary, mbiPayment.getShopMarketDeliveryServices ...
    ...
]);
```
