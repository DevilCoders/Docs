# Кабинет производителя

##### Актуальность зависимостей
[![oko health](https://badger.yandex-team.ru/oko/repo/market/vendors/health.svg)](https://oko.yandex-team.ru/repo/market/vendors)

##### Покрытие юнит тестами
[![Unit test coverage](https://github.yandex-team.ru/pages/market/vendors/coverage.svg)](https://github.yandex-team.ru/pages/market/vendors/coverage)

##### Тулзы
* [diffector](https://github.yandex-team.ru/extg/diffector#readme)
* [testpalm-cli](https://github.yandex-team.ru/extg/testpalm-cli#readme)

### Оглавление

* [Начало работы](#Начало-работы)
* [Сборка и старт сервера](#Сборка-и-старт-сервера)
* [Разработка](#Разработка)
  + [Создание новой страницы](#Создание-новой-страницы)
  + [Actions, Reducers, Selectors and Epics](#actions-reducers-selectors-and-epics)
    - [Actions](#actions)
      * [Action name](#action-name)
      * [Action creator name](#action-creator-name)
      * [Примеры](#Примеры)
      * [Selector name](#selector-name)
    - [Reducers](#reducers)
    - [Epics](#epics)
  + [Работа с ресурсами](#Работа-с-ресурсами)
    - [Конфиги ресурсов](#Конфиги-ресурсов)
  + [Оптимизация изображений](#Оптимизация-изображений)
  + [Структура страниц в ноде](#Структура-страниц-в-ноде)
  + [Версионирование Танкера](#Версионирование-Танкера)
    - [Приоритизация](#Приоритизация)
    - [Управление версиями](#Управление-версиями)
  + [Создание новой услуги](#Создание-новой-услуги)
  + [Динамические настройки](#динамические-настройки)

## Начало работы

Сначала нужно скачать исходники проекта и зависимости в определенную директорию (nginx так настроен). Всё это делается одной командой make_wc на логрусе.
```sh
make_wc
```
Команда запускает визард, в котором нужно сделать следующие действия:
1. Выбрать проект `vendors`
2. Выбрать систему контроля версий на логрусе (git или svn). Инфа про svn: https://docs.yandex-team.ru/marketfront/getting-started/svn, инфа про git: https://docs.yandex-team.ru/marketfront/getting-started/git-shards. Обе документации написаны для проекта marketfront, но в целом, применимы и к вендорскому кабинету.
3. На вопрос
    ```sh
    Would you like to do postinstall? [yes(y)/no(n)]
    ```
   ответить `yes`

Утилита
- скачает файлы проекта
- добавит в вашу домашнюю директорию симлинку на него
- установит зависимости (у вас уже должен быть настроен veendor)
- напишет по какому урлу будет доступен проект после старта сервера

### Сборка и старт сервера
Сервер работает в двух режимах: версия для разработки и продакшн режим. Разница в том откуда грузить статику.
В режиме разработки клиентский код будет загружен с локалхоста (т.е с вашего ноутбука), а в продакшн режиме из той же директории
откуда был запущен сервер.

Из домашней директории по симлинке переходим в корень проекта.

**Для продакшн режима**

1. Собираем статику командой `make`
2. Запускаем сервер `STATIC_SELF=true make server`

Теперь, открыв в браузере кабинет, приложение подключит только что собранную статику.

**Режим разработки**

1. Собираем логрус (в частности, для транспайлинга сервера бабелем)
2. Удаляем на логрусе созданный в корне `manifest.json` (таким образом, статика будет подгружаться с `localhost` по корректным путям)
3. Выполняем на логрусе команду `make server`
4. На локальном компьютере выполняем `npm start`

После того как статика соберется локально, можно открывать логрус.

#### Известные проблемы
**Загрузка статики блокируется браузером**
> Если возникла ошибка `ERR_INSECURE_RESPONSE` при загрузке клиентских бандлов с `https://localhost`,
> откройте бандл в новой вкладке и согласитесь на загрузку из небезопасных источников.
> Для решения проблемы перманентно включите опцию `Allow invalid certificates for resources loaded from localhost.`
> в настройках браузера `chrome://flags/#allow-insecure-localhost`.

**С локалхоста не грузится статика из-за 404**
> Возможно на локальном компьютере у вас не запущен дев сервер. Так же проблема может быть в том, что
> вы, после сборки статики на логрусе, решили включить режим разработки. В этом случае убедитесь,
> что файла manifest.json в корне проекта нет, он нужен только для продакшн сборки

## Разработка

### Создание новой страницы

* Добавьте уникальное имя страницы в [configs/route/routeNames.js](configs/route/routeNames.js)

```js
    MY_NEW_PAGE: 'market-vendors:my-new-page',
```

* Добавьте маршрут в [configs/route/index.js](configs/route/index.js)

```js
{
    name: ROUTE_NAMES.MY_NEW_PAGE,
    pattern: '/path/to/page/<myParam>',
    data: {
        method: 'GET',
        pageName: 'ApplicationHtmlPage',
        pageData: {
            authOnly: true, // Требование авторизации
            vendorOnly: true, // Отображение в меню только при наличии ID вендора в URL
            permissionsOnly: [
                // Ограничение доступа по пермишенаами
                PERMISSIONS.reports.read,
            ],
            menuCaption: true, // Отображение в меню
        },
    },
}
```

> `name` всех новых страниц начинаем с `market-vendors:`
> Для того чтобы страница была доступна **только во внутренней сети**
 нужно указать в `pageData` параметр `isInternalNetworkOnly: true`

* Создайте в [src/pages](src/pages) страницу, например,
 `src/pages/MyNewPage/MyNewPage.js`.

```js
// pages/MyNewPage/index.js
import React, {Fragment} from 'react';

import PageHeading from 'components/PageHeading';

const MyNewPage = () => (
    <Fragment>
        <PageHeading titleKey="pages.my-new-page:title" />
        My new page
    </Fragment>
);

export default MyNewPage;
```

> Относящие только к странице компоненты складывайте в папку со
 страницей: `src/pages/MyNewPage`.

* Добавьте маршрут в [src/Router.js](src/Router.js)

```jsx
<Route name={ROUTE_NAMES.MY_NEW_PAGE} component={MyNewPage} />
```

> `name` в [configs/route/index.js](configs/route/index.js)
 **должен совпадать** с `name` в [src/Router.js](src/Router.js)

### Actions, Reducers, Selectors and Epics

#### Actions

##### Action name

`namespace/[subNamespace/][<NOUN>_]<VERB>[_<STATUS>]`

* `namespace` - Название группы экшнов, обычно имя виджета.
* `subNamespace` - Указывается только, если нужно выделить
  (семантически) некоторые подгруппы экшнов.
* `NOUN` - Указывается только, если область определения несоответсвует
  имени сущности.
* `STATUS = 'FULFILLED' | 'FAILED' | 'CANCELED'` - Указывается только
  для результата асинхронных экшнов.

> Например, `FETCH`, `FETCH_FULFILLED`, `FETCH_FAILED`, `FETCH_CANCELED`


##### Action creator name

`<verb>[<Noun>]`


##### Примеры

```js
// src/actions/myWidget.js

// @flow

import {
    createActions,
    action,
    empty,
} from 'typed-actions';


// Называем переменную без неймспейса и экспортируем.
export const UPDATE = 'myWidget/UPDATE';
export const UPDATE_FULFILLED = 'myWidget/UPDATE_FULFILLED';
export const UPDATE_FAILED = 'myWidget/UPDATE_FAILED';

// НЕ экспортируем!
const actions = createActions({
    // если payload не нужен
    [UPDATE]: empty, // => {type: UPDATE}
    // если есть payload
    [UPDATE_FULFILLED]: (x1: string[], x2: number[], ...args) => action({x1, x2, ...args}), //  => {type: UPDATE_FULFILLED, payload: {x1, x2, ...args}}
    // если есть payload и meta
    [UPDATE_FAILED]: (x: string) => action(/* payload */x, /* meta */{sync: true}), // => {type: UPDATE_FAILED, payload: x, meta: {sync: true}}
});

// Экспортируем получившиеся экшн-креаторы.
export const {
    [UPDATE]: update,
    [UPDATE_FULFILLED]: updateFulfilled,
    [UPDATE_FAILED]: updateFailed,
} = actions;

// Обязательно экспортируйте тип Actions
export type Actions = typeof actions;
```


##### Selector name

`get<Noun>`

Если селектор принимает `props`, то нужно обернуть селектор в функцию,
которая вернет этот селектор, а так же вместо `mapStateToProps`
использовать `makeMapStateToProps`.

[Sharing Selectors with Props Across Multiple Component Instances](https://github.com/reactjs/reselect#sharing-selectors-with-props-across-multiple-component-instances)

> Note: in advanced scenarios where you need more control over the
rendering performance, mapStateToProps() can also return a function.

Source: https://github.com/reactjs/react-redux/blob/master/docs/api.md#arguments


#### Reducers

```js
// src/reducers/widgets/myWidget.js

// @flow

import {type Handlers, handleActions} from 'typed-actions';

import type {State} from 'reducers';
import {
    type Actions,
    UPDATE,
    UPDATE_FULFILLED,
    UPDATE_FAILED,
} from 'actions/myWidget';

export default handleActions(({
    [UPDATE]: state => ({
        ...state,
    }),
    [UPDATE_FULFILLED]: (state, {payload}) => ({
        ...state,
        data: payload,
    }),
    [UPDATE_FAILED]: (state, {payload}) => ({
        ...state,
        error: payload,
    }),
}: Handlers<State, Actions>));
```


#### Epics

```js
// src/epics/widgets/myWidget.js

// @flow

import type {Epic} from 'types/redux';
import type {State} from 'reducers';
import {
    type Actions,
    UPDATE,
    updateFulfilled,
    updateFailed,
} from 'actions/myWidget';

export const updateEpic
    : Epic<State, Actions>
    = action$ => action$
        .ofType(UPDATE)
        .map(() => updateFulfilled())
        .catch(error => updateFailed(error));
```


### Работа с ресурсами

Ресурс - это бекенд. Сейчас используются следущие:
* [report](app/resource/report) - получение "облегченного" списка
моделей (товаров);
* [**vendors**](app/resource/vendors) - основной бекенд, [cпецификация API вендоров](https://github.yandex-team.ru/market/vendors-api-spec);
* [cataloger](app/resource/cataloger.js) - `/getBrandInfo`,
`/getMultipleCategoryNames`;
* [passportMda](app/resource/passportMda.js) - авторизация.


#### Конфиги ресурсов

Все ресурсы находятся в [app/resource](app/resource). Пример конфига:

```js
const config = {
  cfg: {
    maxRetries: 1,
    timeout: 5000,
    agent: {
      name: 'vendors',
    },
  },
  method: 'GET',
  // Ограничения для всех методов
  // Ключи - params передаваемые в метод
  constraints: {
    uid: {presence: true},
  },
  // Параметры которые будут передаваться во всех методы (где не переопрделенно функцией)
  // Ключи то что отправиться в бекенд
  query: {
    uid: 'uid',
  },
  // Дефолтный обработчик результата
  processHandler: result => result,
  // ...
}
```

> В конфиге метода можно доопределить/переопределить любое значение.
Объект доопределяет, функция переопределяет, по принципу `mergeDeep`.
**Доопределение**: `mergeDeep({query: {uid}}, {query: {name}}) -> {query: {uid, name}}`,
**переопрделение**: `mergeDeep({query: {uid}}, {query: () => {}}) -> {query: () => {}}`

Ресурс создается при помощи хелпера [`createResource(config, methods)`](app/resource/createResource.js).
`methods` может быть как коллекцией методов, так и массивом коллекций методов.

```js
// Коллекция методов
const authorities = {
    usersByVendorAndRole: { /* ... */ },
    addRoles: { /* ... */ },
    removeRoles: { /* ... */ },
};

const clients = {
    getClient: {
        path: '/brands',
        constraints:  {
            name: {string: true},
        },
        query: {
            name: 'name',
        },
        processHandler: result => result,
    },
};

// Массив коллекций методов
const methods = [authorities, clients];

const VendorsResource = createResource(config, methods);
```

В результате каждый из методов будет представлять собой полный конфиг, т.е. для получения конечного результата
внутри `createResource` будет использована функция `mergeDeep`, например:

```js
{
    cfg: {
        maxRetries: 3,
        timeout: 5000,
        agent: {
            name: 'vendors',
        },
    },
    path: '/brands',
    constraints:  {
        uid: {precense: true},
        name: {string: true},
    },
    query: {
        uid: 'uid',
        name: 'name',
    },
    processHandler: result => _.get(result, 'result.item'),
    // ...
}
```

[Подробнее о конфигурации создаваемого ресурса](https://github.yandex-team.ru/market/resource-sugar#Конфигурация-создаваемого-ресурса-resourceconfig)


### Оптимизация изображений

Каждое изображение в проекте должно быть оптимизировано,
для этого используется инструмент [svgo](https://github.com/svg/svgo).

```sh
for X in path/to/icons/*.svg; do svgo --enable={removeTitle,removeDesc,removeMetadata,cleanupIDs} "$X" "$X"; done
```

### Структура страниц в ноде
- abstract/BasePage
    - abstract/ApplicationPermissionsPage
        - abstract/ApplicationApiPage
            - api/ApiAnalytics
            - api/ApiAsyncReports
            - api/ApiAuthorities
            - api/ApiBalance
            - api/ApiBanners
            - api/ApiBrandEditRequests
            - api/ApiBrandzone
            - api/ApiCategories
            - api/ApiCutoffs
            - api/ApiEntries
            - api/ApiFiles
            - api/ApiManager
            - api/ApiMarketAnalyticsDemoAccess
            - api/ApiMarketAnalyticsOffer
            - api/ApiMarketingCampaigns
            - api/ApiModelOpinions
            - api/ApiModelQuestions
            - api/ApiModels
            - api/ApiModelsPromotion
            - api/ApiModelsPromotionStatistics
            - api/ApiNotifications
            - api/ApiProducts
            - api/ApiRecommender
            - api/ApiRegions
            - api/ApiReports
            - api/ApiResolve
            - api/ApiShops
            - api/ApiShopsStatistics
            - api/ApiSpecialProjects
            - api/ApiSubscribers
            - api/ApiTariffs
            - api/ApiVendors
        - abstract/ApplicationHtmlPage
            - html/Entry
        - html/Index
    - deprecated/BasePermissionsPage
        - deprecated/BaseJsonPage
            - deprecated/JsonApiPage
                - api/ApiCreateEntry
                - api/ApiDeprecatedEntries
                - api/ApiDeprecatedVendors
                - api/ApiGeoBase

### Версионирование Танкера

Для публикации ломающих изменений в [Танкере](https://tanker.yandex-team.ru/?project=MarketVendors&branch=master) (например, удаление кейсета)
добавлена возможность версионирования этих изменений. Каждой публикации локализаций в [Бункере](https://bunker.yandex-team.ru/market-vendors/tanker) присваивается новая версия.

Эта версия может быть передана в параметр `tankerVersion` в любом из указанных мест:
1. в репозитории проекта в файле `config/common.js`;
2. в `settings`-ноде Бункера проекта.

Возможные значения:
- `"latest"`;
- `"stable"`;
- число (например, `1201`).

Первые два – зарезервированные значения Бункера. Число указывается в выпадающем списке Бункера
при сохранении или публикации `tanker`-ноды.

#### Приоритизация

Версия "latest" превосходит любое число. В свою очередь, любое число превосходит "stable".

#### Управление версиями

**В тестинге**

Аналогично для локальной разработки, мультитестинга и БТ.

1. Сохраняем `tanker`-ноду в Бункере.
2. Подставляем сгенерированную версию в свойство `tankerVersion` в файле `config/common.js`.

**В продакшене**

Опция предназначена, чтобы публиковать новые версии Танкера без релиза.

1. Сохраняем `tanker`-ноду в Бункере.
2. Подставляем сгенерированную версию в свойство `tankerVersion` в `settings`-ноде в Бункере.
3. Сохраняем `settings`-ноду.

**Как это работает?**

Из двух версий по [приоритизации](#Приоритизация) будет выбрана самая последняя.

**Важно!** При использовании значения "latest" в качестве одной из версий все остальные будут проигнорированы.

### Создание новой услуги

**1. Обновление словарей**

  + Добавить пермишены услуги в `app/constants/permissions`.
  + Создать новый ключ услуги в `app/constants/products/keys` в соответствии со спецификацией ручки бекенда.
  + Описать услугу в словаре `app/constants/products`, используя созданный ранее ключ.
    - рекомендуется добавить флаг `isNew: true`, чтобы в интерфейсе напротив созданной услуги появился шильдик "NEW"
  + Обновить снепшоты тестов в `app/resolvers/products`.

**2. Пермишены на страницу "Услуги", катофы и пункт меню**

Добавить read-, write- и finance-пермишены услуги:
  + в `configs/route/index.js` для страницы `ROUTE_NAMES.PRODUCTS` в секции `permissionsOnly`;
  + в `configs/route/jsonApi.js` для ручки `vnd-api:get-cutoffs` в секции `permissionsOnly`;
  + в `configs/route/jsonApi.js` для ручки `api:get-products` в секции `permissionsOnly`;
  + в `src/constants/products/permissions` в константу `PRODUCTS_ALLOWED_PERMISSIONS`.

**3. Пермишены на API**

Поддерживаем новую услугу в ручках подключения и редактирования услуги, а так же изменения статуса размещения услуги.

В `configs/route/jsonApi.js`:
  + Для роута `api:set-product-placement` (изменение статуса размещения услуги):
     - добавляем write-пермишен услуги в секцию `pageData.permissionsOnly`;
     - добавляем ключ услуги в секцию `conditions.productKey`.
  + Для роута `api:get-payment-link` (получение ссылки на пополнение счёта в Балансе):
     - добавляем finance-пермишен услуги в секцию `pageData.permissionsOnly`.
  + Для роута `api:transfer-money` (перевод средств между услугами):
     - добавляем finance-пермишен услуги в секцию `pageData.permissionsOnly`.
  + Для роута `api:get-available-sum-for-transfer` (запрос доступного баланса услуги при переводе средств):
     - добавляем finance-пермишен услуги в секцию `pageData.permissionsOnly`.

**4. Блок услуги на странице "Услуги"**

Блок появится автоматически после обновления словаря, но отсутствие модальных окон
подключения/редактирования услуги будут вызывать Runtime Error.

  + В `src/constants/products/groups.js` добавляем ключ услуги в нужную группу.
  + В `src/constants/products/helpers.js` добавляем связь ключа и пермишенов услуги:
    - в юнит-тестах описываем тест-кейс для новой услуги.
  + В `src/pages/Products/ProductsGrid/Product/Details/ManagerForm/ProductForms` добавляем экспорт формы подключения/редактирования услуги:
    - поддерживаем юнит-тесты в `src/pages/Products/ProductsGrid/Product/Details/ManagerForm`.
  + В `src/pages/Products/ProductsGrid/Product/Details/ManagerViews` добавляем экспорт формы просмотра менеджерской информации услуги:
    - поддерживаем юнит-тесты в `src/pages/Products/ProductsGrid/Product/Details`.
  + В `src/pages/Products/ProductsGrid/Product/SetPlacementModal/SetPlacement` определяем компонент изменения статуса размещения услуги:
    - прописываем связь с `productKey` в `src/pages/Products/ProductsGrid/Product/SetPlacementModal`.
  + В `src/epics/widgets/products/index.js` добавляем ключ и селектор доступности услуги для запроса списка катофов:
    - покрываем юнит-тестом.

**5. Управление пользователями услуги на странице "Настройки"**

  + В `app/constants/authorities.js` заводим роль пользователя услуги.
  + В `src/selectors/widgets/authorities` добавляем связь роли и read-, write-пермишенов услуги:
    - покрываем юнит-тестом.
  + В `src/pages/Settings/Content/Users/AccessByProducts` добавляем блок управления пользователями.

  Добавить write-пермишены услуги:
  + в `configs/route/jsonApi.js` для ручки `api:set-balance-client-logins` в секции `permissionsOnly`;

  Добавить read-пермишены услуги:
  + в `configs/route/jsonApi.js` для ручки `api:get-balance-client-logins` в секции `permissionsOnly`;

**6. Добавление новых маркетинговых услуг (опционально)**

Дополнительно добавляем ключ услуги в константы:
+ `app/constants/marketingCampaigns.js`
+ для пункта меню страницы `ROUTE_NAMES.MARKETING_SERVICES` в `src/components/Menu/index.js`
+ для фильтра по МУ в `src/constants/marketingCampaigns/filters.js`

Пермишены:
+ read-, write-пермишены услуги в `configs/route/index.js` для страницы `ROUTE_NAMES.MARKETING_SERVICES` в секции `permissionsOnly`;
+ write-пермишены услуги в `configs/route/index.js` для страницы `ROUTE_NAMES.MARKETING_SERVICES_CAMPAIGNS` в секции `permissionsOnly`;
+ пермишены услуги в `configs/route/jsonApi.js` в секции `permissionsOnly` для ручек:
  + `vnd-api:get-marketing-campaign` - read-, write-пермишены;
  + `vnd-api:update-marketing-campaign` - write-пермишены;
  + `vnd-api:approve-marketing-campaign` - write-пермишены;
+ write-пермишен для отображения контекстного меню у кампании в `src/pages/MarketingServices/List/withContextMenuShow/index.js`

### Динамические настройки
Для поэтапной раскатки новой функциональности в КВ добавлено управление доступностью страниц кабинета при помощи настроек в Бункере.
В Бункере настройки лежат [здесь](https://bunker.yandex-team.ru/market-vendors/settings/functional-switchers).
Узел в Бункере представляет собой JSON, генерящийся по описанной схеме, которая лежит [здесь](https://bunker.yandex-team.ru/market-vendors/settings/functional-switchers/schema).
Каждую настройку можно сконфигурировать для нужного окружения - development, testing, prestable или production.

#### Как это работает?
На данный момент поддерживается только управление доступностью страниц целиком.
Настройка влияет на загрузку страницы по прямому урлу (обрабатывается на ноде, в декораторе `app/decorators/CheckRouteAccess.ts`), на отображение соответствующего пункта меню (логика в `src/components/HOC/withDisplayRoute/index.js`) и на переключение вендоров в саджесте в заголовке (эпик `vendorChange` в `src/epics/widgets/currentView/index.js`).
Чтобы настройка проросла на клиент, список настроек из Бункера пробрасывается в initial state приложения в резолвере `resolveInitialState` в `app/resolvers/initialState/index.js`.

#### Добавление новой настройки
1. Добавляем новую настройку в Бункере
   1. Для этого нужно открыть [схему](https://bunker.yandex-team.ru/market-vendors/settings/functional-switchers/schema) и добавить в неё новую настройку с уникальным именем (в примере это `your-setting-unique-key`) в секцию `properties`, например:
```json
{
    "properties": {
        "your-setting-unique-key": {
            "title": "Название настройки",
            "definitions": {
                "setting": {
                    "type": "object",
                    "properties": {
                        "isEnabled": {
                            "title": "Страница отображается",
                            "type": "boolean",
                            "default": false
                        },
                        "vendorIds": {
                            "title": "Доступно вендорам (если список пустой, доступно всем вендорам)",
                            "type": "array",
                            "items": {
                                "type": "number",
                                "min": 0
                            }
                        }
                    }
                }
            },
            "type": "object",
            "properties": {
                "development": {
                    "type": "object",
                    "title": "Настройки для разработки (логрусы)",
                    "$ref": "#/properties/your-setting-unique-key/definitions/setting"
                },
                "testing": {
                    "type": "object",
                    "title": "Настройки для тестинга (демо-стенды, БТ, престейбл)",
                    "$ref": "#/properties/your-setting-unique-key/definitions/setting"
                },
                "prestable": {
                    "type": "object",
                    "title": "Настройки для prestable",
                    "$ref": "#/properties/your-setting-unique-key/definitions/setting"
                },
                "production": {
                    "type": "object",
                    "title": "Настройки для production",
                    "$ref": "#/properties/your-setting-unique-key/definitions/setting"
                }
            }
        }
    }
}
```
После сохранения схемы в [JSON с настройками](https://bunker.yandex-team.ru/market-vendors/settings/functional-switchers) появится секция для новой настройки со значениями по умолчанию.
Значения настроек можно редактировать, при сохранении все настройки станут доступны на development и testing-окружениях, при публикации настройки начнут действовать на prestable и production.
1. Описываем тип новой настройки в `entities/settings/types.ts` и добавляем его в общий тип настроек `Setting`;
2. Добавляем новую настройку в константу `SETTINGS` в `app/constants/settings`, в константе `SETTINGS_DEFAULT_VALUES` описываем значение настройки по умолчанию, которое будет использоваться, если настройки от Бункера по какой-то причине не доедут в приложение;
3. Описываем логику доступа к роуту в хэлпере `getRouteAccesses` в `app/helpers/routes/index.ts`, покрываем её юнит-тестами.
