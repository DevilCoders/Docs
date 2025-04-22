# ginny-helpers

[![Version][version-image]](package.json)
[![Flow coverage][flow-coverage-image]](CONTRIBUTING.md#Проверки)
[![Test coverage][test-coverage-image]](CONTRIBUTING.md#Проверки)
[![Dependencies][dependencies-image]](package.json)
[![devDependencies][dev-dependencies-image]](package.json)
[![peerDependencies][peer-dependencies-image]](package.json)
[![Node][node-image]](package.json)
[![License MIT][license-image]](LICENSE)

Хелперы для работы с Ginny в автотестах Market Partner.

* [makePageSuite](#makepagesuite)
* [makePO](#makepo)
* [describe](#describe)
* [getRequireSuite](#getRequireSuite)
* [resolve](#resolve)
* [plugins](#plugins)
* [Типы](#Типы)
* [WebdriverIO & Ginny API](#webdriverio--ginny-api)
* [Конфиг](#Конфиг)
* [Разработка](#Разработка)
* [License](#license)

## makePageSuite

Создаёт страничный сьют по декларации.
Пример декларации со всеми полями:
```jsx
import {App, Checkbox, Header, Icon, Input, Form, Label, Modal} from './pageObjects';
import {defaultBids, settingsLinks} from './suites';

const {RadioBox} = resolve('~/containers/RadioBox');

/**
 * Чтобы извлечь тип контекста из страничного сьюта, сохраняем сьют в переменную.
 */
const pageSuite = module.exports = makePageSuite({
    title: 'Страница заявок на поставку',
    afterEach: async ctx => {...},
    afterPageLoad: async () => {...},
    beforeEach: async ctx => {...},
    environment: 'testing',
    feature: 'Красный Маркет',
    tags: ['red', 'supplier'],
    pageObjects: {
        app: {PO: App},
        checkbox: ctx => ({PO: Checkbox, parent: ctx.app, root: Modal}),
        header: ctx => ({PO: Header, parent: ctx.browser, root: RadioBox}),
        icon: {PO: Icon, parent: Form, root: 'root'},
        input: {PO: Input, parent: 'parent'},
        label: {PO: Label},
    },
    /**
     * Все используемые параметры нужно указать на верхнем уровне
     * (тогда они попадут в общий тип ctx.params), а на уровне каждого сьюта
     * переопределять или стирать (передавая в поле значение undefined).
     */
    params: {
        feedId: 13987,
        page: 'market-partner:html:fulfillment-supply:get',
        shop: getTestingShop(...),
    },
    paramsDescription: {
        role: 'Роль пользователя',
    },
    severity: 'minor',
    suites: [{
        afterEach(ctx) {...},
        beforeEach: ctx => {...},
        params: {
            feedId: 1234,
            shop: getTestingShop(...),
        },
        paramsDescription: {
            feedId: 'Фид',
            supplier: 'Поставщик',
        },
        suite: settingslinks,
        titlePrefix: 'при открытии попапа должны',
    }, {
        suite: defaultBids,
    }],
});

/**
 * Тип контекста страницы экспортируется для использования в сьютах.
 * Переменные частями в контексте являются pageObjects и params.
 */
export type Ctx = typeof pageSuite.context;
````
Пример декларации только с обязательными полями:
```jsx
import {links} from './suites';

const pageSuite = module.exports = makePageSuite({
    pageObjects: {},
    params: {},
    title: 'Страница Качества',
    suites: [{
        suite: links,
    }],
});

export type Ctx = typeof pageSuite.context;
```
Декларация должна содержать заголовок (название страницы) и хотя бы один сьют.
(Поля `pageObjects` и `params` для корректной типизации нужно добавлять, даже если они пустые.)
В поле `params` желательно указать все параметры, которые будет использовать тест, хотя бы с дефолтными значениями
(тогда у поля `params` в контексте теста будет правильный тип).

У сьюта обязательным является только поле `suite`, содержащее (блочный) сьют.

Общестраничные `params` и `paramsDescription` мержатся на `params` и `paramsDescription` каждого сьюта.

Для получения в контексте теста инстанса `PO` нужно задать либо функцию, принимающую контекст теста, и возвращающую
объект с полем `PO` (конструктор `PO`) и необязательными полями `parent` и `root`, с которыми должен вызываться
конструктор для получения инстанса `PO`, либо сразу такой объект.
В качестве `parent` можно указать любой тип селекторов — строку, `PO` (будет использован его рутовый селектор),
`WEP` или `react`-компонент, зарезолвленный `reselector`-ом.
В качестве `root` можно указать только строку или `react`-компонент, зарезолвленный `reselector`-ом.

`paramsDescription` к отсутствующим параметрами игнорируются.

Общие `paramsDescription` (ко всем страницам) можно задать или переопределить в поле `commonParamsDescription`
конфига `ginny-helpers` (по умолчанию заданы описания для `page`, `query`, `shop`, `url`, `user`).

При передаче в параметрах непустого значения `skip` (`ctx.params.skip = 'Пока нельзя проверить...'`)
тест пропускается с указанием причины из параметра.

`titlePrefix` дописывается к заголовку сьюта — его нужно указывать при повторном импорте одного и того же сьюта,
поскольку все сьюты должны иметь разные заголовки.

Хелперы `getUrlForOpen` и `getUserForLogin`, задаваемые в конфиге `ginny-helpers`, получают контекст теста,
и должны вернуть адрес для открытия страницы и пользователя для логина (или `null` — в этом случае логин и/или
переход на страницу произведены не будут).

По умолчанию (то есть, если `getUrlForOpen` не переопределена в конфиге) адрес берётся из параметра `url`
(то есть из `ctx.params.url`), а если такого поля нет,
адрес вычисляется из параметров `page` (роут страницы) и `query` с помощью команды `buildUrl`
(если `query` не передан, но передан `shop`, используется дефолтное значение `query`: `{id: shop.campaignId}`).
Если `url` был вычислен, перед выполнением теста будет открыта страница с этим адресом.

Пользователь по умолчанию (то есть, если `getUserForLogin` не переопределена в конфиге) берётся из параметра
`user`, а если его там нет — из `shop.contacts.owner` (или `shop.contacts.agency` для агентств).
Хелперы `getUrlForOpen` и `getUserForLogin` могут работать и асинхронно, возвращая промис с нужным значением.
Если пользователь был вычислен, то перед выполнением теста (и перед открытием страницы) будет произведён
залогин под этим пользователем.

Если пользователь не задан, а адрес задан, страница откроется без предварительного логина — но только в случае,
если адрес задан напрямую в параметре `url`, а не в виде роута (`page`).

Хук `beforeEach` выполняется до загрузки страницы, и хук `afterPageLoad` — сразу после загрузки.
Все хуки принимают первым аргументом контекст теста, и должны возращать промис со значением `undefined`,
ожидающий завершения всех асинхронных операций в них.

[↑ Наверх](#ginny-helpers)

## makePO

Создаёт `PO` по декларации.
Декларация состоит из четырёх частей (`innerPO`, `selectors`, `selectorsWithParams`, `methods`),
все они обязательны, но в них обязательным полем является только `root` в `selectors`
(значением `root` должна быть строка). Таким образом, минимальная декларация имеет вид:
```jsx
export default makePO({
    innerPO: {},
    selectors: {root: '.my-po'},
    selectorsWithParams: {},
    methods: {},
});
```

Пример декларации со всеми полями и вариантами их заполнения:
```jsx
import {Modal} from 'spec/pageObjects/b2b');

import Affix from './Affix';
import Form from './Form';

const {Spinner} = resolve('b2b/Spinner');
const {Toasts} = resolve('b2b/Toasts');
const {RadioBox} = resolve('~/containers/RadioBox');
const {WizardSteps} = resolve('~/containers/WizardSteps');

export default makePO({
    innerPO: {
        affix: {PO: Affix, parent: WizardSteps, root: '.steps'},
        firstForm: {PO: Form},
        secondForm: po => ({PO: Form, parent: po.toasts, root: '.disabled'}),
        modal: po => ({PO: Modal, parent: Form, root: po.form}),
    },
    selectors: {
        root: '.my-root',
        form: '.form',
        input: PO => `${PO.form} input`,
        button: () => 'button',
        spinner: Spinner,
        radioBox: () => RadioBox,
        popup: {selector: '.popup', global: true},
        toasts: () => ({selector: Toasts, global: true}),
        popupButton: PO => ({selector: `${PO.popup} button`, global: true}),
    },
    selectorsWithParams: {
        submit: PO => type => `.submit ${PO.button} ${type}`,
        content: () => size => `.content ${size}`,
        managerText: PO => nth => ({selector: `${PO.foo} .text ${nth}`, global: true}),
        link: () => ({href, text}) => ({selector: `${text} ${href}`, global: true}),
        tooltip: PO => (type, message) => PO.by`${Tooltip} ${type} ${message}`,
    },
    methods: {
        clickButton: po => [() => po.button.click()],
        getOfferName: po => ['get offer name', async () => {
            const name = await po.popup.getText();

            return `offer ${name}`;
        }],
        getValue: () => ['method description', () => Promise.resolve(12)],
        setFormFields: po => [name => `fields ${name}`, (name, count) => {
            if (name) return Promise.resolve(count);

            return po.m();
        }],
        closeAll: po => [
            'закрыть все попапы',
            () => po.popup.click(),
        ],
        /**
         * Если передать в качестве описания пустую строку,
         * метод не будет обёрнут в allure-шаг.
         */
        save: po => ['', () => po.button.click()],
    },
});
```

`innerPO` создают геттеры инстансов внутренних `PO`. Геттеры устанавливаются на инстанс создаваемого `PO`,
в данном случае это будут `po.affix`, `po.firstForm`, `po.secondForm` и `po.modal`;
значениями этих геттеров являются инстансы `PO`. Инстанс внутреннего `PO` описывается либо объектом
с обязательным полем `PO` (конструктор `PO`) и необязательными полями `parent` и `root`
(аргументы конструктора `PO`), либо функцией, принимающей инстанс родительского `PO` (то есть `po`),
и возвращающей такой объект.

В качестве `parent` можно указать любой тип селекторов — строку, `PO` (будет использован его рутовый
селектор), `WEP` или `react`-компонент, зарезолвленный `reselector`-ом.
В качестве `root` можно указать только строку или `react`-компонент, зарезолвленный `reselector`-ом.
Если не указать `parent` явно, по умолчанию в качестве него будет использован `browser`
(то есть рутовый элемент будет искаться во всём документе).

`selectors` создают геттеры селекторов на `PO` (в данном случае это `PO.root`, `PO.form`, `PO.input`, `PO.button`,
`PO.spinner`, `PO.radioBox`, `PO.popup`, `PO.toasts` и `PO.popupButton`; значениями этих геттеров являются
строки) и соответствующие геттеры элементов на инстансе `PO` (`po.root`, `po.form`, `po.input`, `po.button`,
`po.spinner`, `po.radioBox`, `po.popup`, `po.toasts` и `po.popupButton`;
значениями этих геттеров являются `WEP`, то есть
[`WebElementPromise`](https://seleniumhq.github.io/selenium/docs/api/javascript/module/selenium-webdriver/index_exports_WebElementPromise.html)).
По умолчанию элементы ищутся внутри рутового элемента (`po.root`). Элементы с глобальными
селекторами (у которых указано `global: true`) ищутся внутри всего документа (в данном случае это `po.popup`
и `po.popupButton`).

`selectorsWithParams` создают методы получения селекторов на `PO` (в данном случае это `PO.submit(type)`,
`PO.content(size)`, `PO.managerText(nth)`, `PO.link({href, text})` и `PO.tooltip(type, message)`; значениями
этих методов являются строки) и соответствующие методы получения элементов на инстансе `PO` (`po.submit(type)`,
`po.content(size)`, `po.managerText(nth)`, `po.link({href, text})` и `po.tooltip(type, message)`; значениями
этих методов являются `WEP`). Все элементы, кроме тех, у селекторов которых указано `global: true`,
ищутся внутри рутового элемента.

`methods` создают произвольные методы на инстансе `PO` (в данном случае это `po.clickButton()`, `po.getValue()`,
`po.setFormFields(name, count)` и `po.closeAll()`; значениями методов должны быть промисы).
Методы должны производить на странице действия с инстансом `PO` и возвращать промис (возможно,
с данными — текстом из инпута, количеством элементов, и т.д.). Вызов каждого метода оборачивается в allur-шаг
с заданным описанием действия метода (если описание не задано явно, оно генерируется с помощью функции
`getDefaultMethodDescription` из конфига) и возращённого результата. Можно избежать оборачивания метода в шаг,
передав в качестве описания метода пустую строку.

**Важно!** Методы в целом не должны возвращать `WEP` (для этого есть `selectorsWithParams`).
Если в методе по какой-то причине требуется вернуть `WEP` (например, асинхронная логика выбора селектора),
метод не должен быть `async`-функцией (иначе `WEP` обернётся в промис).

[↑ Наверх](#ginny-helpers)

## describe

Функция `describe` позволяет создать (блочный) сьют.

Пример со всеми полями:
```jsx

/**
 * Тип контекста страницы импортируется из страничного сьюта.
 * Переменные частями в контексте являются pageObjects и params.
 */
import type {Ctx} from '..';

export default describe<Ctx>({
    afterEach: async () => {...},
    beforeEach: async () => {...},
    title: 'Промо-блок',
    environment: 'testing',
    feature: 'Красный Маркет',
    issue: 'MARKETPARTNER-8471',
    severity: 'blocker',
    tags: ['red'],
}, it => {
    it({
        title: 'Футер присутствует',
        environment: 'all',
        feature: 'Прогнозатор',
        id: 'marketmbi-1188',
        issue: 'MARKETPARTNER-8268',
        severity: 'normal',
        skip: 'Будет включён после фикса',
        tags: 'price-center',
    }, async ctx => {
        ctx.expect(ctx.page.footer.isVisible()).equal(true, 'футер выводится');
    });

    it({
        title: 'Удаление региона происходит без ошибок',
        environment: 'kadavr',
        feature: 'Прогнозатор',
        id: 'marketmbi-1238',
        issue: 'MARKETPARTNER-8263',
        severity: 'minor',
        tags: ['cpc', 'smoke'],
    }, async ctx => {
        ...
    });
});
```

Пример только с необходимыми полями:
```jsx
import type {Ctx} from '..';

export default describe<Ctx>({
    title: 'Валидация контрола Тип организации',
}, it => {
    it({title: 'Контрол присутствует', id: 'marketmbi-1189'}, async ctx => {
       ...
    });

    it({title: 'Контрол переключается', id: 'marketmbi-1190'}, async ctx => {
       ...
    });
});
```

Необходимым полем в `describe` является только заголовок (`title`; вместо объекта с полями можно указать
только строку с заголовком), в `it` необходимыми являются заголовок и `id` (у каждого теста должен быть свой
`id`, и `id` нельзя передавать в `describe`).

При этом для каждого `it`-теста должны быть определены поля `environment`, `feature` и `issue` — либо на уровне
`describe`, либо в самом `it` (значения из `it` приоритетнее; значения из страничного сьюта имеют наименьший
приоритет, и даже если `environment` или `feature` определены в страничном сьюте, каждый блочный сьюта
должен сам определять эти поля).

При указании поля `skip` у `it` тест будет пропущен с указанной в поле причиной (то есть попадёт в скипнутые
 в `allur`-отчёте).

Теги, указанные в `tags` на уровне `describe`, добавляются к тегам, указанным в `it`.

Все тесты асинхронны — функция теста (второй аргумент в `it`) принимает контекст теста и должна возвращать промис,
разрешающийся после всех асинхронных действий и проверок.

Хуки `afterEach` и `beforeEach` должны возращать промис, ожидающий завершения всех асинхронных операций в них.

Вызов `describe` не может вкладываться в `describe` и `it`, вызов `it` не может вкладываться в другой `it`.

Кроме того, в `describe` нужно передавать тип контекста для данной страницы (`Ctx`), экспортируемый из страничного
сюта (тип включает `pageObjects` и `params`, которые задаются именно в страничном сьюте).

[↑ Наверх](#ginny-helpers)

## getRequireSuite

Используется только в `./suites/index.js` для импорта (реэкспорта) блочных сьютов с правильной типизацией,
и для разрыва циклической зависимости типов страничного и блочного сьютов:
```jsx
/**
 * requireSuite работает как require, но с типизацией и проверкой импортируемого значения.
 */
const requireSuite = getRequireSuite(require);

export const groups = requireSuite('./groups');
export const offers = requireSuite('./offers');
export const settings = requireSuite('./settings');
```

Если импортируется не блочный сьют, бросает исключение.

[↑ Наверх](#ginny-helpers)

## resolve

Заменяет `resolve` из `reselector`. Не требует оборачивания пути в `require.resolve`, бросает исключение,
если импортируемого компонента нет в модуле (даже если сам модуль найден по пути) и поддерживает алиасы из
поля `resolverAliases` в конфиге:
```jsx
const {Button} = resolve('b2b/Button');
const {Search} = resolve('~/pages/Auction/components/Search');
const {PaymentModal} = resolve('~/components/PaymentModal');

// TypeError: module "~/components/PaymentModal" does not have component "NotExistingComponent"
const {NotExistingComponent} = resolve('~/components/PaymentModal');
```

[↑ Наверх](#ginny-helpers)

## plugins

* **itParams** – после подключения, позволяет устанавливать параметры теста (`user`, `shop`, `query` и т.д.) внутри `it`.
Для этого нужно добавить их в поле `currentParams`:
```js
// ...
it(
    {
        title: 'title',
        id: 'id',
        issue: 'issue',
        currentParams: {
            user: getUser('user'),
            shop: getTestingShop('shop'),
            query: {
                id: getTestingShop('shop').campaignId,
            },
        },
    },
    () => {},
);
// ...
```
Важный момент. В конфиге гермионы в `suiteManager.metaTags` должен быть упомянут параметр `currentParams`:
```js
// ...
    suiteManager: {
        // ...
        metaTags: [
            //..
            'currentParams',
            //..
        ],
        // ...
    },
// ...
```
* **viewportSize** – позволяет в параметрах подключения установить дефолтный размер вьюпорта для тестов

[↑ Наверх](#ginny-helpers)

## Типы

`ginny-helpers` экспортирует следующие `flow`-типы:
* `Allure` — объект `allure` в `browser` и в контексте теста
* `AnyInstanceOfPO` — произвольный инстанс `PO` (созданного с помощью `makePO`)
* `AnyPO` — произвольный `PO` (созданный с помощью `makePO`)
* `Browser`— объект `browser` (в `PO` и в контексте теста)
* `Config` — тип конфига из `ginny-helpers.config.js`
* `Context` — контекст теста (содержит `allure`, `browser`...) без `pageObjects` и `params`
* `Environment` — окружение (`testing`, `kadavr`, `all`, ...)
* `PageObject` — `PageObject` из `ginny`
* `Params` — параметры теста (`ctx.params`)
* `Severity` — приоритет теста, из TestPalm (`blocker`, `minor`, ...)
* `Shop` — магазин как объект в тестовых данных (утилитарный тип для ПИ)
* `User` — пользователь Яндекса как объект в тестовых данных
* `WEP` — `WebElementPromise`, то есть инстанс, содержащий методы `click`, `getText`, ...

[↑ Наверх](#ginny-helpers)

## WebdriverIO & Ginny API

Вместе с `ginny-helpers` на элементах рекомендуется использовать только следующие методы `WEP`:
```jsx
/**
 * Кликнуть по элементу.
 */
wep.click(): Promise<Element> {}

/**
 * Получить значение атрибута элемента по имени атрибута
 * (возвращает null, если такого атрибута нет).
 */
wep.getAttribute(attribute: string): Promise<string | null> {}

/**
 * Получить массив со значениями атрибута нескольких элементов по имени атрибута
 * (если атрибута на элементе нет, значением является пустая строка).
 */
wep.getAttributes(attribute: string): Promise<string[]> {}

/**
 * Получить вычисленное значение css-свойства соответствующего DOM-элемента (по имени свойства).
 */
wep.getCssProperty<P: string>(cssProperty: P): Promise<{+property: P, +value: string}> {}

/**
 * Получить размеры элемента в пикселях (объектом с полями width и height).
 */
wep.getElementSize(): Promise<{|+width: number, +height: number|}> {}

/**
 * Получить HTML-код элемента.
 * Если includeSelectorTag равен true, то в код будет включён и тег самого элемента.
 */
wep.getHTML(includeSelectorTag?: boolean = true): Promise<string> {}

/**
 * Получить координаты левого верхнего угла элемента (в пикселях).
 * Точка (0, 0) — левый верхний угол страницы.
 */
wep.getLocation(): Promise<{|+x: number, +y: number|}> {}

/**
 * Получить тип (имя тега) соответствующего DOM-элемента.
 */
wep.getTagName(): Promise<string> {}

/**
 * Получить текстовое содержимое элемента.
 */
wep.getText(): Promise<string> {}

/**
 * Получить массив с текстовым содержимым нескольких элементов, найденных по одному селектору.
 */
wep.getTexts(): Promise<string[]> {}

/**
 * Получить текущее значение контрола (input-а, select-а).
 */
wep.getValue(): Promise<string> {}

/**
 * Получить массив текущих значений контролов (input-ов, select-ов), найденных по одному селектору.
 */
wep.getValues(): Promise<string[]> {}

/**
 * Получить булев флаг видимости элемента (вместо isExisting).
 * Несуществующие элементы и элементы с display: none; или visibility: hidden; считаются невидимыми.
 * Остальные элементы, существующие на странице (в том числе скрытые за границами viewport,
 * чем-то перекрытые или полностью прозрачные) считаются видимыми.
 */
wep.isVisible(): Promise<boolean> {}

/**
 * Кликнуть по элементу с указанием смещения от его левого верхнего угла в пикселях.
 */
wep.leftClick(xoffset: number, yoffset: number): Promise<Element> {}

/**
 * Переместить курсор в центр элемента. Если указаны смещения xoffset и yoffset (вместе),
 * курсор будет перемещён в точку с этим смещением относительно левого верхнего угла элемента.
 */
wep.moveToObject(xoffset?: number, yoffset?: number): Promise<void> {}

/**
 * Ввести текст в input или textarea. Контрол должен находиться во viewport
 * (чтобы можно было поставить в него курсор).
 * Предыдущий текст в контроле будет предварительно очищен.
 */
wep.setValue(value: string): Promise<void> {}

/**
 * Дождаться видимости (или невидимости) элемента, с проверкой раз в полсекунды.
 * Если элемент не появился за заданное время, возвращённый промис реджектится.
 * Если элемент появился, возвращённый промис резолвится значением true.
 * Если флаг reverse равен true, ожидается, наоборот, скрытие элемента (по умолчанию false).
 * Несуществующие элементы и элементы с display: none; или visibility: hidden; считаются невидимыми.
 * Остальные элементы, существующие на странице (в том числе скрытые за границами viewport,
 * чем-то перекрытые или полностью прозрачные) считаются видимыми.
 */
wep.waitForVisible(timeout?: number = 500, reverse?: boolean = false): Promise<true> {}
```

На объекте `browser` рекомендуется использовать только следующие методы `WEP` и команды:
```jsx
/**
 * Подтвердить открытый alert (то есть кликнуть кнопку OK в нативном диалоговом окне браузера).
 */
browser.alertAccept(): Promise<void> {},

/**
 * Выбрать локальный файл в элементе <input type=file>.
 * selector должен быть полным селектором нужного инпута.
 * В localPath должен быть локальный абсолютный путь к загружаемому файлу
 * (файл должен лежать в системе, на которой запущен тест).
 */
browser.chooseFile(selector: string, localPath: string): Promise<void> {},

/**
 * Закрыть текущее окно (таб). Полезно при кликах на ссылки, открывающиеся в новых окнах.
 */
browser.close(): Promise<void> {},

/**
 * Остановить выполнение теста для дебага.
 * При этом терминал превращается в REPL-интерфейс, позволяющий
 * пошагово выполнять любые команды и проверки: http://webdriver.io/images/repl.gif
 * Аргумент commandTimeout устанавлиет таймаут для выполнения команд в REPL-интерфейсе.
 */
browser.debug(commandTimeout?: number = 5000): Promise<void> {},

/**
 * Запуск синхронной функции fn с единственным параметром params (произвольное JSON-значение с WEP)
 * на клиенте. Возвращаемое из fn значение (JSON-значение с DOM-элементами) вернётся (в промисе и в value)
 * с заменой DOM-элементов на WEP.
 */
browser.execute(fn: (params: P) => R, params: P): Promise<{|+value: R|}> {},

/**
 * Запуск асинхронной функции fn с единственным параметром params (произвольное JSON-значение с WEP)
 * на клиенте. Переданное во второй аргумент (коллбек done) JSON-значение (с DOM-элементами) вернётся
 * (в промисе и в value) с заменой DOM-элементов на WEP.
 */
browser.executeAsync(fn: (params: P, done: R => void) => void, params: P): Promise<{|+value: R|}> {},

/**
 * Получить объект cookie по имени.
 */
browser.getCookie(name: string): Promise<Cookie> {},

/**
 * Получить адрес текущей страницы.
 */
browser.getUrl(): Promise<string> {}

/**
 * Ввести в input (или textarea) текст посимвольно.
 * Ввод осуществляется в элемент, находящийся в данный момент в фокусе.
 * Текстовые коды клавиш: https://w3c.github.io/webdriver/#keyboard-actions
 */
browser.keys(keys: string[]): Promise<void> {}

/**
 * Обновить (перегрузить) страницу, как по клавише F5.
 */
browser.refresh(): Promise<void> {},

/**
 * Выставить на странице cookie.
 */
browser.setCookie(cookie: Cookie): Promise<void> {},

/**
 * Записать в стейт Кадаврика по заданному пути (ключу) нужное значение.
 */
browser.setState(path: string, data: mixed): Promise<void> {},

/**
 * Изменить размер viewport или окна.
 * type = true — установить размер viewport.
 * type = false — установить размер окна (viewport будет чуть меньше из-за рамок, статус-бара, меню).
 */
browser.setViewportSize(size: {|+width: number, +height: number|}, type: boolean): Promise<void> {},

/**
 * Проскроллировать страницу до указанного положения.
 */
browser.scroll(xoffset: number, yoffset: number): Promise<void> {},

/**
 * Или проскроллировать страницу до указанного элемента, с опциональным дополнительным смещением.
 */
browser.scroll(selector: string, ?number, ?number): Promise<void> {},

/**
 * Установить максимальное время выполнения соответствующей операции  Webdriver.
 * 'script' — время выполнения клиентского скрипта.
 * 'pageLoad' — время загрузки страницы.
 * 'implicit' — время поиска элемента (WEP) на странице.
 */
browser.timeouts(type: 'script' | 'pageLoad' | 'implicit', ms: number): Promise<void> {},

/**
 * Дождать, пока функция-условие вернёт true, с таймаутом и с заданным интервалом проверки.
 * Если условие не вернёт true за заданное время, возвращённый промис реджектится.
 */
browser.waitUntil(
    condition: () => Promise<boolean>,
    timeout?: number = 500,
    timeoutMsg?: string,
    interval?: number = 500,
): Promise<void> {},
```

Здесь объект `Cookie` имеет тип:
```jsx
type Cookie = {|
    name: string,
    value: string,
    path?: string,
    domain?: string,
    secure?: boolean,
    httpOnly?: boolean,
    expiry?: number,
|};
```

В контексте теста рекомендуется использовать следующие методы и свойства:
```jsx
/**
 * Приложить к allure-отчёту произвольное значение (под заданным заголовком).
 */
ctx.attach(name: string, value: mixed): void {}

/**
 * Приложить к allure-отчёту JSON (под заданным заголовком).
 */
ctx.attachJSON(name: string, json: mixed): void {}

/**
 * Приложить к allure-отчёту скриншот текущего состояния страницы (только viewport).
 * Заголовок можно не указывать (по умолчанию — Screenshot).
 */
ctx.attachScreenshot(name?: string = 'Screenshot'): Promise<void> {}

/**
 * Объект browser.
 */
ctx.browser: Browser,

/**
 * Проверить произвольное значение (в том числе значение в промисе).
 * Возвращает промисифицированную цепочку ассертов chai: https://www.chaijs.com/plugins/chai-as-promised/
 * Перед вызовом expect всегда должен стоять await.
 */
ctx.expect(value: mixed | Promise<mixed>): Assertion {},

/**
 * Объект с мета-данными текущего теста (environment, severity, feature, id, issue...).
 */
ctx.meta: {|
    environment?: Environment,
    feature?: string,
    id: string,
    issue?: string,
    severity?: Severity,
    tags?: Tags,
|},

/**
 * Параметры, с которыми был запущен (блочный) сьют.
 * Стандартные параметры (все они необязательны): page, query, shop, url, user.
 * Помимо них можно указывать любые параметры, нужные в тестах сьюта.
 */
ctx.params: Params,

/**
 * Пропустить тест с указанием причины: return ctx.skip('Будет включён после фикса');
 */
ctx.skip(reason: string): void {},

/**
 * Алиас для ctx.browser.allure.runStep(...).
 */
ctx.step(name: string, body?: (...args: A) => R = () => {}, ...args: A): R {},
```

[↑ Наверх](#ginny-helpers)

## Конфиг

`ginny-helpers` может настраиваться с помощью необязательного конфига, лежащего в корне проекта по пути
`ginny-helpers.config.js`.
Все поля в конфиге необязательны, и при отсутствии принимают дефолтные значения (если конфига нет,
каждое поля примет дефолтное значение).

Полный конфиг с дефолтными значениями имеет вид:
```jsx
module.exports = {
    before: undefined,
    beforeEach: undefined,
    commands: {
        buildUrl: 'yaBuildURL',
        login: 'yaLogin',
        logout: 'yaLogout',
        openPage: 'yaOpenPage',
    },
    commonParamsDescription = {
        page: 'Страница',
        query: 'query-параметры страницы',
        shop: 'Магазин',
        url: 'Адрес страницы',
        user: 'Пользователь',
    },
    getDefaultMethodDescription: (ctx, methodName, ...args) => `Вызываем ${methodName}(${args})`,
    getUrlForOpen: ctx => {...},
    getUserForLogin: ctx => {...},
    log: undefined,
    PO: PageObject,
    resolverAliases: {
        '~': 'client.next',
        b2b: '@yandex-market/b2b-components/src/components',
    },
};
```
`before` — если эта функция задана, то она будет вызвана один раз перед запуском первого теста с текущим
контекстом в качестве единственного аргумента. Как и все хуки, функция должна возвращать промис
со значением `undefined`.

`beforeEach` — если эта функция задана, то она будет вызываться перед запуском каждого теста с текущим
контекстом в качестве единственного аргумента. Как и все хуки, функция должна возвращать промис
со значением `undefined`.

Функция `getDefaultMethodDescription` принимает контекст, название метода, и все аргументы метода, и возвращает
дефолтное описание метода в `allure`-шаге, которое будет использовано, если для метода не указано собственное
описание.

Маппинг команд используется для логина, открытия страниц, построения адреса из роута страницы, и для разлогинивания
(в конце каждого теста). Помимо строки, команду можно явно указать в виде функции (она примет первым аргументом
контекст, и далее те же аргументы, что и соответствующая `ya`-команда).

`log` — если эта функция задана, то она вызывается при различных событиях (поиск элемента, вызов методов `po`,
вызов переопределённых методов `webdriverio`, резолв компонентов с помощью `reselector`) с единственным аргументом
(объектом, содержащим строковое поле `type` с типом события, и некоторый набор остальных полей, зависящий от типа).

Типы логируемых событий:
 * `AFTER_METHOD_CALL`: выход из вызванного метода (методы — `attach`, `by`, `step`...)
 * `AFTER_PO_METHOD_CALL`: выход из вызванного метода `PO`
 * `BEFORE_METHOD_CALL`: вход в вызванный метод (методы — `attach`, `by`, `step`...)
 * `BEFORE_PO_METHOD_CALL`: вход в вызванный метод `PO`
 * `CALL_IS_VISIBLE`: вызов метода `wep.isVisible`
 * `CALL_PIPED_GETTER`: вызов piped-метода у `wep` (`getAttributes`, `getTexts`, `getValues`)
 * `CALL_SET_VALUE`: вызов метода `wep.setValue`
 * `CALL_WAIT_FOR_VISIBLE`: вызов метода `wep.waitForVisible`
 * `CREATE_INSTANCEOF_PO`: создание инстанса `PO`
 * `CREATE_PAGE_SUITE`: создание страничного сьюта
 * `CREATE_PO`: создание `PO`
 * `CREATE_SUITE`: создание (блочного) сьюта
 * `RESOLVE_COMPONENT`: резовл реакт-компонента реселектором
 * `SEARCH_ELEMENT`: поиск `wep` по селектору в инстансе `PO`
 * `SEARCH_ROOT_ELEMENT`: поиск рутового `wep` (`po.root`) на инстансе `PO`

`PO` — класс (расширяющий исходный `PageObject`), который будет использоваться в качестве родителя при создании
PO хелпером `makePO`, при этом сам `PO` расширяется следующими обязательными методами:
```jsx
class ExtendPO extends PO {
    /**
     * Приложить к allure-отчёту произвольное значение (под заданным заголовком).
     */
    attach(name: string, value: mixed): void {
        this.browser.allure.createAttachment(name, inspect(value));
    }

    /**
     * Приложить к allure-отчёту JSON (под заданным заголовком).
     */
    attachJSON(name: string, json: mixed): void {
        this.browser.allure.createAttachment(name, JSON.stringify(json, null, 2), 'application/json');
    }

    /**
     * Приложить к allure-отчёту скриншот текущего состояния страницы (только viewport).
     * Заголовок можно не указывать (по умолчанию — Screenshot).
     */
    async attachScreenshot(name?: string = 'Screenshot'): Promise<void> {
        const {value: screenshot} = await this.browser.screenshot();

        this.browser.allure.createAttachment(name, Buffer.from(screenshot, 'base64'));
    }

    /**
     * Алиасы для функции select из reselector, но с проверкой переданных в селектор значений.
     * Допустимые значения: строка, финитное число и реакт-компонент, зарезолвленный методом resolve.
     */
    static by(strings: string[], ...values: any): string {
        assertSelectValues(values);

        return select(strings, ...values);
    }

    by(strings: string[], ...values: any): string {
        assertSelectValues(values);

        return select(strings, ...values);
    }

    /**
     * Получить инстанс PO из конструктора и опциональных рута и родителя
     * (как в innerPO и pageObjects).
     */
    getInstanceOfPO({PO. parent, root}: {
        PO: AnyPO, parent?: string | WEP | AnyInstanceOfPO, root?: string | ReselectorComponent,
    }): AnyInstanceOfPO {
        return new PO(this.browser, paretn, root);
    }

    /**
     * Получить видимость po (то есть рутового элемента этого po).
     */
    isVisible(): Promise<boolean> {
        return this.root.isVisible();
    }

    /**
     * Алиас для свойства constructor (которое flow не типизирует верно).
     */
    get PO(): AnyPO {
        return ExtendPO;
    }

    /**
     * Получить актуальный селектор рута
     * (то есть с учётом возможного переопределения рута в конструкторе).
     */
    get rootSelector: string {
        return this._root || declaration.root;
    }

    /**
     * Алиас для ctx.browser.allure.runStep(...).
     */
    step(name: string, body?: (...args: A) => R = () => {}, ...args: A): R {
        return this.browser.allure.runStep(name, body, ...args);
    }

    /**
     * Дождаться видимости (или невидимости) po (то есть рутового элемента этого po).
     */
    waitForVisible(timeout?: number = 500, reverse?: boolean = false): Promise<true> {
        return this.root.waitForVisible(timeout, reverse);
    }
}
```
Остальные поля конфига описаны в [makePageSuite](#makepagesuite) и [resolve](#resolve).

[↑ Наверх](#ginny-helpers)

## Разработка
- [Changelog](CHANGELOG.md)
- [Contributing](CONTRIBUTING.md)

## License
[MIT](LICENSE)

[flow-coverage-image]: https://img.shields.io/badge/flow%20coverage-95%25-green.svg?longCache=true&style=flat-square "Flow coverage"
[test-coverage-image]: https://img.shields.io/badge/coverage-92%25-green.svg?longCache=true&style=flat-square "Test coverage"
[dependencies-image]: https://img.shields.io/badge/dependencies-2-brightgreen.svg?longCache=true&style=flat-square "Dependencies"
[dev-dependencies-image]: https://img.shields.io/badge/devDependencies-17-brightgreen.svg?longCache=true&style=flat-square "devDependencies"
[peer-dependencies-image]: https://img.shields.io/badge/peerDependencies-11-brightgreen.svg?longCache=true&style=flat-square "peerDependencies"
[node-image]: https://img.shields.io/badge/node->=12.16-brightgreen.svg?longCache=true&style=flat-square "Node"
[license-image]: https://img.shields.io/badge/license-MIT-blue.svg?longCache=true&style=flat-square "The MIT License"
[version-image]: https://img.shields.io/badge/version-0.29.0-blue.svg?longCache=true&style=flat-square "Version"
