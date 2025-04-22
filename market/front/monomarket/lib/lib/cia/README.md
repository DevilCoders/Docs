[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/cia)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/cia) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/cia)](https://oko.yandex-team.ru/pkg/@yandex-market/cia)

# cia

Данный пакет содержит вспомогательные модули для работы с «новой» метрикой, основанной на зонах -- мета-информации
о том, в каком контексте произошло событие или экшен. Этот пакет также позволяет настроить логирование данных в
[Baobab](https://wiki.yandex-team.ru/baobab/) \
Как работать с зонами в проектах смотрите в
[Документации по метрике (+ воркшоп)](https://wiki.yandex-team.ru/Market/frontend/workshops/react-metric/).

- [Зоны-на-React](#Зоны-на-React)
  - [Zone](#Zone)
    - [свойства (`props`)](#zone-props)
    - [withZone](#withZone)
    - [withConnectedZone](#withConnectedZone)
  - [Baobab](#Baobab)
  - [ClickSensor](#ClickSensor)
  - [VisibilitySensor](#VisibilitySensor)
    - [withVisibilitySensor](#withVisibilitySensor)
    - [withConnectedVisibilitySensor](#withConnectedVisibilitySensor)
  - [createZonedPortal](#createZonedPortal)
  - [emitter](#emitter)
  - [Метрика в статических виджетах](#Метрика-в-статических-виджетах)
    - [Инициализация статических сенсоров](#Инициализация-статических-сенсоров)
- [Зоны на BEM](#Зоны-на-BEM)
  - [b-zone](#b-zone)
  - [b-spy-visible](#b-spy-visible)
  - [b-spy-events](#b-spy-events)
  - [b-spy-init](#b-spy-init)
  - [Метрика](#Метрика)

## Зоны на React

Зоны собираются через DOM, что обеспечивает работоспособность при работе на прогрессивных страницах и в статичных виджетах.
Для оборачивания компонентов в зону используются компонент `Zone` и HOC-и `withZone`/`withConnectedZone`.

## Zone

### <a id="zone-props"></a>Свойства (`props`)

- `name: string` - Имя зоны.
- `baobabNodeId?: string` - Предустановленный id баобаб узла. Используется для залогированных на сервере узлов
- `baobabName?: string` - Название узла баобаба. Если не указано - берется имя зоны из поля `name`. Нужно, когда название зоны баобаба отличается от имени зоны метрики.
- `applyToRootChild?: boolean` – Применить зону к корневому дочернему элементу.
(Работает только с единственным дочерним узлом, который является реальным  DOM-элементом.)

  [Презентация по решаемой проблеме и параметру](https://jing.yandex-team.ru/files/pilyugin/Zones%20wo%20wrappers.pdf)
- `withClickSensor?: boolean` – Включение сбора метрики кликов по вложенным в зону элементам.
- `clickActionName?: string` – Название action'а, который будет отправлен при клике (default: 'click'). Не влияет на `mode: 'baobab'`.
- `withVisibilitySensor?: boolean` – Включение сбора метрики видимости зоны.
- `visibilityThreshold?: number | number[]` – Доля видимой площади зоны, при которой срабатывает метрика видимости. Число от 0 до 1. Подробнее в документации [`IntersectionObserver.thresholds`](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/thresholds)
- `data?: mixed` – Данные, которые будут отправлены с метрикой.
- `allowPrivateActions?: boolean` – разрешаем отправку приватных экшнов в метрику
- `mode?: 'metrika' | 'baobab' | 'both'` - отвечает за способ конфигурации зоны. `'metrika'` - конфигурирует зону для отправки событий только в Я.Метрику, `'baobab'` - только в Баобаб, `'both'` - и в Я.Метрику и в Баобаб (default: `'metrika'`)
- `calcCoords?: boolean` - Флаг, который указывает нужно ли расчитывать координаты элемента и записывать их в атрибуты Baobab-узла. Работает только в mode="baobab" и mode="both"
- `className?: string`
- `cacheKey?: string` - кеширует Баобаб-узел по переданному ключу. В случаи ремаунта компонента, новый узел не будет создан. [Подробнее](#Baobab)

Пример использования
```js
import {Zone} from '@yandex-market/cia';

const ZonedProductSnippet = props => (
    <Zone name="productSnippet" data={{productId: props.productId}}>
        <ProductSnippet {...props}/>
    </Zone>
);
```

**ВНИМАНИЕ**: По умолчанию `Zone` оборачивает дочерние компоненты в `div`.
С определенными ограничениями можно использовать свойство `applyToRootChild`, чтобы применить зону без обертки.

### withZone

`withZone(settings: string | ZoneHocSettings<P>, mapPropsToZoneData?)`
- `settings` – название зоны или объект настроек (все `props` компонента `Zone`, кроме `data` и `applyToRootChild`)
- `mapPropsToZoneData` – функция, принимающая на вход `props` из родительского компонента
- `mapPropsToCacheKey` - функция создания ключа кеширования Баобаб-узла по `props`-ам. [Подробнее](#Baobab)
и возвращающая `data` для зоны.

#### <a id="hoc-settings"></a>Расширенные настройки (`type ZoneHocSettings<P>`)
Где `P` - пропсы оборачиваемого компонента
- `name: string` - Имя зоны.
- `baobabNodeId?: string` - Предустановленный id баобаб узла. Используется для залогированных на сервере узлов-
- `baobabName?: string` - Название узла баобаба. Если не указано - берется имя зоны из поля `name`. Нужно, когда название зоны баобаба отличается от имени зоны метрики.
- `withClickSensor?: boolean` – Включение сбора метрики кликов по вложенным в зону элементам.
- `clickActionName?: string` – Название action'а, который будет отправлен при клике (default: 'click'). Не влияет на `mode: 'baobab'`.
- `withVisibilitySensor?: boolean` – Включение сбора метрики видимости зоны.
- `visibilityThreshold?: number | number[]` – Доля видимой площади зоны, при которой срабатывает метрика видимости. Число от 0 до 1. Подробнее в документации [`IntersectionObserver.thresholds`](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/thresholds)
- `data?: mixed` – Данные, которые будут отправлены с метрикой.
- `mode?: 'metrika' | 'baobab' | 'both'` - отвечает за способ конфигурации зоны. `'metrika'` - конфигурирует зону для отправки событий только в Я.Метрику, `'baobab'` - только в Баобаб, `'both'` - и в Я.Метрику и в Баобаб (default: `'metrika'`)
- `calcCoords?: boolean` - Флаг, который указывает нужно ли расчитывать координаты элемента и записывать их в атрибуты Baobab-узла. Работает только в mode="baobab" и mode="both"
- `className?: string | (props: P) => string | undefined` - имя CSS класса или функция, его возвращающая на основе пропсов оборачиваемого компонента

Простое оборачивание компонента в зону:

```js
import {withZone} from '@yandex-market/cia';

const mapStateToProps = (state, ownProps) => ({
    name: getProductName(state),
    price: getProductPrice(state),
});

const mapDispatchToProps = (dispatch, ownProps) => ({
    onClick: clickProduct,
});

const ZonedProductSnippet = compose(
    withZone('productSnippet'),
    connect(mapStateToProps, mapDispatchToProps)
)(ProductSnippet);
```

Оборачивание в зону с прокидыванием данных от props-ов контейнера:

```js
import {withZone} from '@yandex-market/cia';

const mapPropsToZone = ownProps => ({
    zoneId: ownProps.id,
});

const ZonedProductSnippet = compose(
    withZone('productSnippet', mapPropsToZone),
    connect(mapStateToProps, mapDispatchToProps)
)(ProductSnippet);
```

Использование HOC'а с дополнительными параметрами зоны:
```js
const ZonedComponentWithSensors = withZone({
    name: 'productSnippet',

    withClickSensor: true,
    clickActionName: 'navigate',

    withVisibilitySensor: true,
    visibilityThreshold: 0.5,
    allowPrivateActions: true,
})(SomeComponent);
```

### withConnectedZone

Оборачивает компонент в зону с доступом к стейту (виджетному или обычному-реактовому):

```js
import {connect} from 'react-redux';
import {withConnectedZone} from '@yandex-market/cia';

const mapStateToZone = (state, ownProps) => ({
    pageName: getPageName(state),
});

const mergeProps = (stateProps, dispatchProps, ownProps) => ({
    pageName: stateProps.pageName,
    zoneId: ownProps.zoneId,
})

const ZonedProductSnippet = compose(
    // Обязательно передать mergeProps, иначе все пропсы (собственные и из mapStateToZone) улетят в метрику
    withConnectedZone('productSnippet', connect(mapStateToZone, null, mergeProps)),
    connect(mapStateToProps, mapDispatchToProps)
)(ProductSnippet);
```

Аналогично работает с виджетным `connect`:
```js
import {connect} from '@yandex-market/apiary';
import {withConnectedZone} from '@yandex-market/cia';

const mapDataToZone = (state, ownProps) => ({
    pageName: getPageName(state),
});

const mergeProps = (stateProps, dispatchProps, ownProps) => ({
    pageName: stateProps.pageName,
    zoneId: ownProps.zoneId,
})

const ZonedSomePage = compose(
    // Обязательно передать mergeProps, иначе все пропсы (собственные и из mapStateToZone) улетят в метрику
    withConnectedZone('somePage', connect(mapStateToZone, null, mergeProps)),
    connect(mapDataToProps)
)(SomePage);
```

**ВНИМАНИЕ** Старайтесь использовать `withConnectedZone`, когда действительно необходима cвязь данных зоны со стором.

## Baobab

Баоба собирает 2 вида логов - структурные логи и логи событий. Структурные логи - это логи изменения дерева. Соответственно,
логеру нужно построить связанную структуру узлов (дерево), залогировать его во время инициализации приложения и логировать
любое изменение дерева (добавление/удаление узлов). Логи событий - это либо лог клика по узлу (click), либо лог скрола узла (scroll), либо лог
технического (tech) события, ассоциированного с узлом. Лог события не содержит в себе весь путь до узла, на котором произошло
событие - он содержит только id узла.

Баобаб-узлы собираются по размеченным зонам с настройкой `mode: "both"` или `mode: "baobab"`. Во главе баобаб дерева всегда
должен быть root-узел. Root-узел - это узел с `name="$page"` и атрибутами `ui` и `service`
[смотри сюда](https://wiki.yandex-team.ru/baobab/rfc/common/#zarezervirovannyeatributy). Если root-узла в дереве не будет -
дерево не соберется. Если "выше" root-узла будут другие узлы, они будут интерпретироваться как другое несвязанное дерево.

Для инициализации баобаб логера необходимо использовать статичный метод `configure` класса `Baobab`. Конфигурацию
нужно проводить во время инициализации приложения (до монтирования первых зон).

В некоторых ситуациях реакт компонент может ремаунтится, например, в случаи виртуализации. Чтобы исключить
добавление новых Baobab-узлов в случаи ремаунта компонентов, можно указать атрибут `data-node-cache-key`. По этому ключу
будет найден существующий Baobab-узл и залогировано событие появления.

```js
import {Baobab, Sender} from '@yandex-market/cia';

Baobab.configure("some-requestId", Sender, {hrefPrefix: "...", hrefPostfix: "..."});
```

Для конфигурации нужно передать текущий `requestId`. По нему будут генерироваться уникальные идентификаторы баобаб узлов.
Также нужно передать класс `Sender` (не инстанс). В этом классе описаны методы отправки различных событий в баобаб.
Можно использовать стандартную реализацию, а можно описать класс, наследуемый от стандартного `Sender` и переопределить
нужные методы. Третий параметр - это объект аргументов конструктора `Sender`. В этом объекте должны обязательно
содержаться поля `hrefPrefix` и `hrefPostfix`. `hrefPrefix` - это url отправки событий, а `hrefPostfix` - postfix, который
добавляется к каждому событию, например `/*//yandex.ru` для СЕРП-а.

## ClickSensor

Компонент `ClickSensor` собирает метрики кликов по вложенным в зону элементам.
По сути то же самое, что и `Zone` с параметром `withClickSensor`, но без добавления зоны.

### Свойства (`props`)

- `actionName?: string` – Название action'а, который будет отправлен при клике (default: `'click'`). Не влияет на `mode: 'baobab'`.
- `className?: string`
- `applyToRootChild?: boolean` – Применить сенсор к корневому дочернему элементу.
(Работает только с единственным дочерним узлом, который является реальным  DOM-элементом.)

> Note: Работает в статических виджетах.

Пример:
```js
    <ClickSensor actionName="navigate">
        <a {...linkProps}>some link</a>
    </ClickSensor>
```

**ВНИМАНИЕ** - отправка метрик в Баобаб осуществляется от имени ближайшего родительского баобаб-узла.

## VisibilitySensor

Для отправки в метрику признака видимости элемента внутри зоны оборачиваем нужный контент в `VisibilitySensor`:

```js
import {VisibilitySensor} from '@yandex-market/cia';

const SomeSnippet = ({title, onClick}) => (
    <VisibilitySensor>
        <div>
            <span>{title}</span>
            <button onClick={onClick}>Click me!</button>
        </div>
    </VisibilitySensor>
);
```

**ВНИМАНИЕ**:
1. Компонент `VisibilitySensor` НЕ работает в статических виджетах.
Для работы метрики видимости в статических виджетах используйте свойство зоны `withVisibilitySensor`
2. Для работы `VisibilitySensor` необходимо, чтобы у него был единственный дочерний компонент.
3. В Баобаб метрика отправляется техническим событием от имени ближайшего родительского баобаб-узла.

### withVisibilitySensor

Оборачивает компонент в `VisibilitySensor`:

```js
import {withVisibilitySensor} from '@yandex-market/cia';

export default compose(
    withVisibilitySensor(),  // можно передать параметры.
    connect(mapStateToProps)
)(SomeSnippet);
```

### withConnectedVisibilitySensor

Оборачивает компонент в `VisibilitySensor` с доступом к стейту (виджетному или обычному-реактовому):

```js
import {withConnectedVisibilitySensor} from '@yandex-market/cia';

const mapStateToSensorProps = (state, ownProps) => ({
    ...
});

export default compose(
    withConnectedVisibilitySensor(connect(mapStateToSensorProps), options /* можно передать параметры */),
)(SomeSnippet);
```

## createZonedPortal

Аналог ReactDom-овского метода createPortal, который умеет сохранять вложенность зон.

```js
import * as React from 'react';
import {Zone, createZonedPortal} from '@yandex-market/cia';
import {ChildComponentThatUsesZones, ModalChildComponentThatUsesZones} from './components';

const Component = props => (
    <Zone name="veryImportantZone" data="{'veryImportantFlag': 1}">
        <ChildComponentThatUsesZones />
        {
            createZonedPortal(
                <ModalChildComponentThatUsesZones />,
                document.getElementById('modalContainerthatHelpsWithZIndex')
            )
        }
    </Zone>
)
```

## emitter

### meta

Есть несколько параметров в meta, которые влияют на общее поведение при отправке метрики:
1. `ignoreZone` - метрика отправляться не будет
2. `withSyncMetrikaCall` - вызывать отправку метрики синхронно. Не влияет на `mode: 'baobab'`.

## Метрика в статических виджетах

В статических виджетах есть возможность собирать метрики видимости и кликов.
Для этого нужно:
1. Проинициализировать статические сенсоры (см. пример ниже).
2. Использовать
   - сенсоры через свойства `Zone` (именно props зоны, а не одноименные HOC'и):
`withClickSensor`/`withVisibilitySensor` (см. описание `Zone`).
   - для сбора кликов без добавления дополнительной зоны можно использовать компонент `ClickSensor`.

Презентация: https://jing.yandex-team.ru/files/pilyugin/Static%20cia.pdf

### Инициализация статических сенсоров

Вызываем `initSensors` при инициализации страницы в браузере:
```typescript
import {initSensors} from '@yandex-market/cia';
import type {GenericAction} from '@yandex-market/apiary/common/actions';

function emitMetrika(action: GenericAction) {
  // реализация отправки action'a в метрику
}

// Если нужно настроить сенсоры для отправки событий в Баоба
const withBaobab: boolean = true;

initSensors(emitMetrika, withBaobab);
```

## Зоны на BEM

При реализации метрики для новых блоков или рефакторинге старых, в большинстве случаев необходимо применять *зоны*.

### b-zone

Блок можно превратить в «зону», подмиксовав к нему виртуальный блок `b-zone` и добавив в объект внутри `data-bem` настройки этого блока.

Блок `b-zone` принимает один обязательный конфигурационный параметр `name` — имя зоны, и один опциональный параметр `data` — объект с некоторой дополнительной информацией о зоне.

Боевой пример:
```html
<body class="b-page b-page__body b-zone n-base i-global i-ua_js_yes i-bem">
    @data-bem = n-serialize({
        "n-base": ""
        "b-zone": {
            "name": "{.page.id}_PAGE"
        }
    })
    ...
</body>
```

Так как в метрику улетают bem-события, то необходимо иметь js реализацию блока, которая и выбрасывает событие. В некоторых распространённых случаях это превращается в рутину. Для упрощения разметки поставляются несколько вспомогательных блоков — хелперов, которые выбрасывают события.

### b-spy-visible

[Данный блок](src/spies/visible.js) выбрасывает событие `visible`, когда блок становится видимым пользователю.

Видимость определяется как одновременное выполнение следующих условия:
* Заданная точка блока находится во viewport-е.
* Блок не скрыт (`display: none` или `visibility: hidden`).
* Блок не закрыт другим блоком.

Пример использования:
```html
<div class="b-spy-visible i-bem" data-bem='{"b-spy-visible": {}}'>
    <p>Здесь могла быть ваша реклама, пишите <b>b-vladi@mail.ru</b></p>
</div>
<div class="b-spy-visible i-bem" data-bem='{"b-spy-visible": {"mode":{"x": 0.2, "y": 0.5}}'>
    <p style="width: 200px; height: 300px;">Здесь могла быть ваша реклама, пишите <b>b-vladi@mail.ru</b></p>
</div>
<div class="b-spy-visible i-bem" data-bem='{"b-spy-visible": {"mode":{"dx": 100, "dy": 250}, {"data":{"foo": "bar"}'>
    <p style="width: 200px; height: 300px;">Здесь могла быть ваша реклама, пишите <b>b-vladi@mail.ru</b></p>
</div>
```

Данный блок принимает параметры:
1. `mode` — точка (`{"x": 0.5, "y": 1, "dx": 100, "dy": 1}` любой из параметров может отсутствовать) или название пресета (`center`, `topLeft`, `topRight`, `bottomLeft`, `bottomRight`). Если параметр не задан или задан несуществующий пресет, то используется `center` (`{"x" 0.5, "y": 0.5, "dx": 0, "dy": 0}`).
2. `data` - объект с некоторой дополнительной информацией о событии.

Позиция точки вычисляется по формулам:
```javascript
    const desired; // указанная точка в bem параметрах
    const mode = {
            x: desired.x == null ? .5 : desired.x,
            y: desired.y == null ? .5 : desired.y,
            dx: desired.dx || 0,
            dy: desired.dy || 0,
        };
    const rect = element.getBoundingClientRect();
    const x = rect.left + (rect.right - rect.left) * mode.x + mode.dx;
    const y = rect.top + (rect.bottom - rect.top) * mode.y + mode.dy;
```
Принцип работы блока следующий: при инициализации блок добавляется в глобальный [вотчер](src/watcher.js), который по скроллу, таймеру и фокусу проверяет все отслеживаемые блоки. Если у объекта нет b-zone, то ключ метрики будет сформирован на основе родительской метки b-zone. Для точки проверяется, что она находится в видимой области и не перекрыта другим блоком.

```html
<div class="b-spy-visible i-bem" data-bem='{"b-zone": {"name":"example"}}'>
    <div class="some-class">
        <p data-bem='{"b-spy-visible": {}}'>Здесь могла быть ваша реклама, пишите <b>b-vladi@mail.ru</b></p>
    </div>
</div>
```
Метрика будет `example_visible`

### b-spy-events

[Данный блок](src/spies/events.js) нужен для отслеживания DOM-событий и их ретрансляции как BEM-событий.

**ВНИМАНИЕ**: использование данного блока является антипаттерном, так как теряется семантика событий (вместо `addToCart` появляется `click` на кнопке).

Пример использования:
```html
<div class="b-spy-events i-bem" data-bem='{"b-spy-events": {}}'>
    <p>Здесь могла быть ваша реклама, пишите <b>b-vladi@mail.ru</b></p>
</div>
```

При клике на данном блоке произойдёт BEM-событие `click`.

Данный блок принимает один опциональный параметр `events` — массив с именами отслеживаемых DOM-событий. В случае, если параметр не задан, то отслеживаются только клики.

Блок инициализируется лениво.

### b-spy-init

Этот блок можно подмиксовать, когда необходимо просигналить в Метрику об инициализации некого блока. Отправляет в Метрику BEM-событие `init`.


### Метрика

TODO: добавить ссылки на реализации реактовой метрики.

Непосредственно о модуле метрики данный пакет ничего не знает, а провязка осуществляется в проектных репозиториях ([тач](https://github.yandex-team.ru/market/mobile/blob/develop/touch.modules/bem-metrika/bem-metrika.js), [десктоп](https://github.yandex-team.ru/market/MarketNode/blob/master/client/desktop.modules/bem-metrika/bem-metrika.js)).

Слушаются все события, возникающие в `BEM.DOM`-блоках. Действия при возникновении очередного события:
1. События фильтруются по чёрному списку.
2. Собираются все зоны от текущего блока и выше.
3. По именам зон (`name`) и имени события формируется цель.
4. Данные зон (`data`) и данные события сливаются вместе, образуя параметры цели.
5. Полученная цель и параметры отсылаются в метрику.

Несмотря на то, что алгоритм одинаков для тача и десктопа, есть различия в чёрном списке и способе формирования цели, которые скрыты по ссылкам выше.

Рассмотрим пример:
```html
<body class="b-zone">
    @data-bem = n-serialize({
        "b-zone": {
            "name": "PRODUCT_PAGE"
            "data": {
                "foo": 1
            }
        }
    })

    <div class="b-zone">
        @data-bem = n-serialize({
            "b-zone": {
                "name": "FOOTER"
                "data": {
                    "bar": 2
                }
            }
        })

        <div class="some-block"></div>
    </div>
    ...
</body>
```

Теперь, если на блоке `some-block` произойдёт событие `someEvent` с параметрами `{kek: 3}`, то в метрику будет отправлена цель `PRODUCT-PAGE_FOOTER_SOME-EVENT` с параметрами `{foo: 1, bar: 2, kek: 3}` (в таче, для десктопа вид цели будет несколько отличаться).
