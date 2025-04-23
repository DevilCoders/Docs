# Виджетная система

**Apiary** — фреймворк для построения прогрессивных страниц, в основе которого лежит декомпозиция приложения на самодостаточные виджеты. В какой-то степени является реализацией HMVC паттерна.

[Презентация с HL++](https://yadi.sk/i/YtIxARVt3YUDAZ ), [Видео](https://www.youtube.com/watch?v=pIQo6yCicQk&feature=youtu.be)

[Видео с внутренним докладом](https://yadi.sk/i/0MROAPYz3UocHd)

## Предпосылки
### Классическая модель

Классическая модель веб-приложений использует подход «запрос-ответ»:

![](resources/classic-model.svg)

Такая модель предполагает последовательное прохождение следующих этапов:
1. Сбор данных на сервере.
2. Шаблонизация на сервере.
3. Доставка данных и вёрстки на клиент.
4. Инициализация на клиенте.

![](resources/classic-timeline.svg)

### Прогрессивная модель

В прогрессивной модели страницы рассматриваются как набор chunk-ов с их постепенной отдачей:

![](resources/progressive-model.svg)

Такую отдачу будем называть **прогрессивной отдачей** (как «прогрессивный JPEG»).

Если во время прогрессивной отдачи происходит инициализация отданных chunk-ов, то называть мы это будем **прогрессивной инициализацией**.

Страницы, реализующие хотя бы прогрессивную отдачу будем называть прогресссивными.

Прогрессивная модель даёт ощутимое преимущество над классической:

![](resources/compare-timeline.svg)

Таким образом,
- Статика начинает грузиться раньше.
- Пользователь видит контент раньше.
- Пользователь может взаимодействовать с контентом раньше.

Задача apiary — предоставить фреймворк для построения таких прогрессивных страниц.

## Принципы

### Уровни приложения

Приложение состоит из трех уровней:
- **Виджет** — отвечает за сбор данных, actions, reducers, epics и отображение самостоятельной части приложения. Для получения данных использует **резолверы**.
- **Резолвер** — позволяет получить данные. Часто использует **ресурсы**.
- **Ресурс** — предоставляет внутренний API для работы с бекендами.

![](resources/widgets-resolvers-resources.svg)

### Виджеты

**Виджет** можно представлять самостоятельным приложением, а **apiary** выступит ОС для него. В виджет инкапсулирована вся логика получения данных, отрисовка и взаимодействие с пользователем.

Виджеты могут выставлять **джобы** или **единицы работы**. Через джобы виджет даёт указание окружению, что он хотел бы сделать. Например, виджет может попросить выставить куку или совершить редирект. Джобы не обязательно будут выполнены.

Любой виджет можно использовать в другом виджете. Родительский виджет размечает **слоты** и указывает, какой виджет в него стоит положить.

Виджет может выбрать среди дочерних **main**-виджет, что даст дополнительную информацию для обработчиков джоб. Цепочку из main-виджетов будем называть **main-путём**.

**В виджет нельзя передавать данные, только конфигурацию (Options). Данные виджет получает для себя сам, используя резолверы.** Если одни и те же данные нужны в разных виджетах, для их получения должен быть использован резолвер с настроенным [кэшированием](https://github.yandex-team.ru/market/partner-cookbook/blob/master/docs/dev/shared-resolvers-caching.md).

Виджеты являются error boundary: ошибки виджета за его пределы не выходят.

Каждый виджет хранит свои данные в **store**, который делит со всеми другими виджетами.

![](resources/common-state.svg)

### Дерево виджетов
Возможность вкладывать виджеты в другие виджеты приводит к появлению //иерархии виджетов//, которая обычно представляется в виде //дерева виджетов//:

![](resources/widget-hierarchy.svg)

Оранжевым цветом показаны main-виджеты.

Если вспомнить, что виджеты могут выставлять различные джобы, то картинка становится следующей:

![](resources/widget-hierarchy-jobs.svg)

Джобы могут выполняться в двух фазах: в **отложенной** (на клиенте) или **блокирующей** (на сервере). Блокирующая фаза получила своё название по той причине, что отдача страницы блокирует до момента выполнения всех джоб блокирующей фазы.

При этом, далеко не все джобы будут выполнены. Например, на это влияет, лежит ли виджет на main-пути или нет. Логика выполнения джоб, фаза выполнения и необходимость выполнения определяется обработчиком каждой конкретной джобы.

![](resources/widget-hierarchy-jobs-done.svg)

<details>
<summary>Процесс отдачи</summary>
<p>

![](resources/widget-hierarchy-stream-0.svg)

![](resources/widget-hierarchy-stream-1.svg)

![](resources/widget-hierarchy-stream-2.svg)

![](resources/widget-hierarchy-stream-3.svg)

![](resources/widget-hierarchy-stream-4.svg)

</p>
</details>


### Серверные события

Апиари, благодаря построению дерева виджетов, позволяет подписываться на определенные события.
Подписка на события происходит по аналогии с [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener).
У поля context.event есть метод addEventListener, с помощью которого можно подписаться на следующие события

- `onWidgetRendered: ({time: number}): void` - вызывается при окончании рендера виджета на сервере и до отправки данных на клиент

## Репозитории

![](resources/repositories-2.svg)

По ссылкам можно видеть TS-типы и описание к ним.

_Flow-типы лежат в [отдельной папке](../flow)_

### apiary

- [Ядро виджетной системы](../../apiary)
- [Клиентская и серверная часть виджетов](../src/common/widget.ts)
- [Виджетный `connect`](../src/common/connect.ts)
- [Виджетный `connectToWidget`](../src/common/connectToWidget.ts)
- Клиентский и серверный инициализатор
- Подсистема обработки джоб
- [Хелперы для определения экшенов](../src/common/actions.ts)
- [Публичный API](../src/index.ts)

### apiary-annex

- [Общие компоненты](https://github.yandex-team.ru/market/apiary-annex)
- [Общие виджеты](https://github.yandex-team.ru/market/apiary-annex/tree/master/src)
- [Обработчики общих джоб (cookie, meta, title, redirect, status)](https://github.yandex-team.ru/market/apiary-annex/tree/master/src/jobs)

### mandrel

- [База проектов](../../mandrel)
- [Стартер клиента и сервера](../../mandrel/src/launchServer)
- [Настройка логгера, apiary, таймеров и так далее](../../mandrel/src/launchClient)
- [Реализация контроллера прогрессивных страниц](../../mandrel/src/progressive)
- [Реализация `/api/resolve` и пр](../../mandrel/src/remoteResolver)
- [Серверный контекст](../../mandrel/src/context/index.js)
- [Клиентский контекст](../../mandrel/src/clientContext.js)
- [Хелперы для работы с резолверами](../../mandrel/src/resolver/index.js)
- [Общие резолверы (stout, page, browser, experiment)](../../mandrel/src/resolvers)

## Файловая структура

Здесь описана структура, к которой следует стремиться.

```sh
src/                          #
  actions/                    # глобальные экшены
  entities/
    product/                  # наименование в единственном числе
      index.js                # типы тоже здесь
      reducer.js
      selectors.js
  epics/                      # глобальные эпики
  resolvers/
      product.js              # наименование в единственном числе
  widgets/
      core/                   # базовые виджеты, не относящиеся к контенту
      layouts/                # виджеты для распределения других виджетов по странице
      pages/                  # страничные виджеты
        SomePage/             # имеют суффикс "Page"
      parts/                  # целые куски. Например, подстраницы на SPA-странице
      content/                # контентные виджеты
        SomeWidget/
          index.js            # типы и Widget.describe
          controller.js       # серверный контроллер виджета
          view.js             # view виджета
          reducer.js          # редьюсер данных виджета
          epics.js            # виджетные эпики
          actions.js          # приватные экшены виджета

  components/
  containers/
  resources/
  utils/                       # различные небольшие вспомогательные модули
```

## Резолверы

[Документация и общие резолверы](../../mandrel/src/resolvers)

[Полезные хелперы](../../mandrel/src/resolver/index.js)

Отдельно стоит упомянуть удалённые резолверы — резолверы, которые могут быть вызваны с клиента. Для этого достаточно при создании резолвера через `createResolver` включить в настройки `remote: true`:

```js
import {createResolver} from '@yandex-market/mandrel/resolver';

export const resolveProductById = createResolver(
    (ctx, id: string) => ...,
    {remote: true}
);
````

Вызов на клиенте практически идентичен вызову на сервере:

```js
import ctx from '@yandex-market/mandrel/clientContext';

import {resolveProductById} from '@/resolvers/product';

resolveProductById(ctx, {productId: 42}).then(...);
```

Несколько важных моментов:
* В контекст из виджетов лазить строго не рекомендуется, для этого стоит использовать резолверы
* Роут и query-параметры берутся той страницы, с которой был вызван резолвер. Значения параметров определяется в момент запроса
* Пока поддерживается только объявление резолверов через `export const someName = createResolver(...)`
* Поддерживается пересылка циклических данных
* В качестве промежуточного формата используется JSON, где не все типы представимы
* Ошибки тоже пересылаются и восстанавливаются довольно близко к оригинальным: с цепочками ошибок, дополнительными свойствами и т.д.
* Запросы отправляются балками, используется окно в несколько мс

## Виджеты

[Виджет Example](https://github.yandex-team.ru/market/marketfront/tree/master/market/src/widgets/content/Example)

[Типы лучше документации](../src/common/widget.ts)

### Жизненный цикл

Виджет проходит следующие этапы:
- `started` - начало выполнения контроллера виджета
- `shaped` - контроллер вернул значение (сформирована схема виджета)
- `registered` - виджет поступил на обработку
- `stuffed` - построен стейт виджета
- `rendered` - виджет отрендерился
- `shipped` - виджет записан в поток
- `arrived` - DOM виджета сформирован
- `inited` - виджет проинициализировался

### Декларация

Виджет декларируется в файле `index.js`:

```js
import {Widget} from '@yandex-market/apiary';

// Подключаем виджеты, которые нам нужны на клиенте.
import '@/widgets/content/SomeWidget';

import globalEpic from '@/epics/someEpic';
import type {Some, SomeId, SomeCollections} from '@/entities/some';
import someReducer from '@/entities/some/reducer';

import controller from './controller';
import view from './view';
import widgetReducer from './reducer';

export type Options = {
    someId: SomeId,
};

// Желательно типы для данных и коллекций тоже определять здесь.
export type Data = {
    someId: SomeId,
};

export type Collections = SomeCollections;

export default Widget.describe({
    name: '@repoName/Example',

    directives: {
        // ...
    },

    view,
    controller,

    reducers: {
        widget: widgetReducer,
        collections: {
            some: someReducer,
        },
    },
    epics: {
        widget: [widgetEpic],
        global: [globalEpic],
    },
});
```

React-виджет — виджет, view которого описывается на react.

Как стоит описывать сущность `Some` в `entities` можно почитать в [доке](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/README.md).

### Контроллер

Контроллер — функция получения и подготовки начального состояния виджета. Выполняется только на сервере и должен всегда располагаться в файле `controller.js`, который выкидывается при сборке для клиента.

**Схема** — возвращаемое значение контроллера. В схеме описываются данные и коллекции, которые нужны виджету, выставляются джобы и описываются слоты. Все составляющие необязательны.

```js
import type {Context} from '@yandex-market/mandrel/context';

import {resolveSome} from '@/resolvers/some';
import SomeWidget from '@/widgets/content/SomeWidget';

import type {Options} from '.';

export default function (ctx: Context, {someId}: Options) { // для flow <0.71 стоит указать * для результата
    const somePromise = resolveSome(ctx, {someId});

    return {
        // Данные виджета. Не шарятся с другими виджетами.
        data: Promise.resolve({someId}),
        // Коллекции общие на все виджеты. Коллекции именуются по entity, которые лежат в ней.
        collections: {
            some: somePromise.then(({collections}) => collections.some || {}),
        },
        main: 'nested',
        slots: {
            nested: SomeWidget.create(ctx, {count: 42}),
        },
        // Выставялем некоторые джобы.
        jobs: [
            ...
        ],
        // делает виджет статичным. Данные статичных виджетов не отправляются на клиент, а сам виджет не инициализируется
        static: true,
    };
}
```

Чтобы свернуть пустой виджет, достаточно вернуть `null` из контроллера.

### React View

```jsx
import React from 'react';
import {connect, Slot} from '@yandex-market/apiary';

import type {Data, Collections} from '.';

// Мапперы имеют схожее поведение с redux-овыми, только по умолчанию возвращают пустой объект.
const mapDataToProps = (data: Data, collections: Collections) => {...};
const mapDispatchToProps = {...};

const Example = ({...}) => (
    <div className="lol">
        <Slot name="nested" />
    </div>
);

export default connect(mapDataToProps, mapDispatchToProps)(Example);
```

View со слотом необходимо обернуть в connect (даже пустой), чтобы клиент определил данные слота и отрендерил его.

### connectToWidget

В дополнение к `connect`, который обеспечивает обработку ошибок и подключение виджета на страницу,
добавлен `connectToWidget` с версии 1.13.0

`connectToWidget` позволяет подключать к данным виджета и виджетному `dispatch` компоненты,
вызываемые внутри виджетной `View`.
Эта возможность нужна, чтобы обойти необходимость прокидывать обернутые виджетным `dispatch`-ем экшены
и данные по всей иерархии компонентов.

`connectToWidget` использует зарезервированную пропу `widgetId`. При её получении извне произойдет ошибка.

```jsx
import React from 'react';
import {connectToWidget as connect, Slot} from '@yandex-market/apiary';

import type {Data, Collections} from '.';

type OwnProps = {prop: number};

// Мапперы имеют схожее поведение с redux-овыми, только по умолчанию возвращают пустой объект.
// По сравнению с обычной версий апиарного `connect`, мапперы принимают prop-ы компонента
const mapDataToProps = (data: Data, collections: Collections, ownProps: OwnProps) => {...};
const mapDispatchToProps = {...};

const Example = ({...}) => (
    <div className="lol">
        <Slot name="nested" />
    </div>
);

export default connect(mapDataToProps, mapDispatchToProps)(Example);
```

### Директивы
- `asyncController` — разрешает контроллеру возвращать промис или быть `async`. Пожалуйста, используйте эту возможность только в случаях, когда иначе написать контроллер не получается. Потому что построение дерева виджетов будет ждать этот виджет, и дерево далее вглубь процессится не будет, что затормозит всю страницу.

В apiary <= 0.14.0 статичные виджеты нельзя вставлять в нестатичные, т.к для статичных виджетов не будут отправлены данные, необходимые для гидрации, а гидрация будет вызвана на всё дерево виджетов, начиная с первого нестатичного.

### Опции слота

При инстанцировании виджета третий параметр отвечает за опции слота:

```js
SomeWidget.create(ctx, widgetOptions, slotOptions);
```

Доступные опции слота:
- `bare` - виджет в слоте не нужно рендерить. Состояние при этом формируется и отсылается с родительским виджетом.
- `measured` - замерять ли виджет. По каждому замеряемому виджету отправляется статистика о времени его прибытии и рендеринге на клиенте, а также определяется: попадает на первый экран он или нет.

Подробнее [здесь](../src/common/widget.ts) - Type SlotOptions

### Экшены

**Глобальные**

Глобальные экшены располагаются в `actions` и обычно определяются как-то так:

```js
import {SimpleAction} from '@yandex-market/apiary';

export const TODO_SMTHNG: '@repoName/some/TODO_SMTHNG' = '@repoName/some/TODO_SMTHNG';
export type TodoSmthng = SimpleAction<typeof TODO_SMTHNG>;
export const todoSmthng = (): TodoSmtng => ({type: TODO_SMTHNG});
```

Ну или любым другим способом. Например, используя [typed-actions](https://github.com/lttb/typed-actions).

Желательно префиксовать такие экшены названием репозитория.

**Приватные**

Приватные экшены располагаются рядом в директории виджета (`actions.js`) и начинаются с `#` (например `#SORT`). Особенностью данных экшенов является то, что их получают только эпики и редьюсеры того инстанса виджета, который и задиспатчил их.

### Редьюсеры

Пример описания виджетного редьюсера:

```js
import {static as Immutable} from 'seamless-immutable';

// ...

export default function (data: Data, action: Action | GlobalAction): Data {
    switch (action.type) {
        case '#DOUBLE':
            const authors = data.authors.concat(data.authors);

            return Immutable.set(data, 'authors', authors);
        case '#REMAIN':
            return Immutable.set(data, 'authors', action.payload);
        default:
            return data;
    }
}
```

Работоспособность не-static варианта `seamless-immutable` не гарантируется.

### Эпики

Пример описания виджетного эпика:

```js
import type {WidgetFacade, WidgetEpic, GlobalFacade, GlobalEpic} from '@/yandex-market/apiary';

// Можно описать, используя WidgetFacade/GlobalFacade:
function someEpic(action$: Observable<GlobalAction | Action>, facade: WidgetFacade): Observable<GlobalAction | Action> { ... }

// А можно использовать WidgetEpic/GlobalEpic типы:
const someEpic: WidgetEpic<GlobalAction | Action, Data, Collections> = (action$, facade) =>
    action$
        .ofType('#DOUBLE')
        .map(action => {
            const {authors} = facade.getData();
            const uniq = Array.from(new Set(authors));

            return {type: '#REMAIN', payload: uniq};
        });

export default [someEpic];
```

Фасады похожи на стор, но только предоставляют доступ к ограниченному набору данных. Для `WidgetFacade` это методы `getData()` для получения данных виджета и `getCollections()` для получения коллекций. Глобальный фасад `GlobalFacade` предоставляет только доступ к коллекциям через `getCollections()`.

Для обновления стора со стороны apiary предоставляется экшен `UPDATE_COLLECTIONS`:

```js
import {updateCollections} from '@yandex-market/apiary';

dispatch(updateCollections({some: ...}))
```

### Теневой redux-стор

При включении опции `useShadowStore` - экшены будут накапливаться до конца тика в т.н. теневом сторе.
По окончании тика - все накопленные экшены будут слиты в основной стор.
Идея оптимизации заключается в том, что вот время накапливания экшенов - view, которые используют этот стор, не реагируют на изменения в нем (не перерисовываются).
Это позволяет сэкономить десятки перерисовок.

`Runtime.run({ ...options, useShadowStore: false | 'always' | 'dcl' })`

- `false` - теневой стор отключен
- `dcl` - теневой стор включен только до наступления DOMContentLoaded
- `always` - теневой стор включен всегда

> Важно помнить, что при включённом теневом сторе, эпики и редьюсеры работают с одним стором (который обновляется сразу), а view с другим (который будет обновлен в конце тика)

> Таким образом, внутри эпиков/редьюсеров недопустимо завязываться на DOM-дерево, которое генерируется view, т.к. оно всегда будет запаздывать

### Очередь гидрации

По умолчанию виджеты гидрируются на странице по мере отработки скрипта обработки патча,
которые появляются по мере появления виджетов в потоке HTML.
Такое может приводить к тому, что браузер склеит все гидрации виджетов в одну синхронную таску EventLoop.

Опция `useHydrationHeap`, переданная в клиентски рантайм Apiary, запустит асинхронную очередь гидрации.
Если какая-то одна гидрация, или несколько подряд идущих, не укладывается в окно (по умолчанию `30ms`),
то следующие гидрации будут отложены на последующие шаги EventLoop.

При этом появляется возможность управлять приоритетом гидрации. Т.е. некоторые виджеты проинициализируются
и обзаведутся коллбэками вперёд остальных. Этим поведением управляет параметр `hydrationPriority`, переданный в схеме контроллера
Чем больше значение параметра, тем более приоритетным будет виджет. По умолчанию все виджеты имеют нулевой приоритет.

```js
Runtime.run({
    useHydrationHeap? : false | {
        // Откладываем старт гидрации насколько-то ms.
        // Иногда это удобно, т.к. позволяет разгрузить поток инициализации страницы
        startDelay? : number,
        // Если придёт виджет с высоким приоритетом (`>= priorityForceStart`), то стартуем немедленно
        priorityForceStart? : number,
    },
})

```


## Вложенность виджетов

Теперь о том, какие виджеты можно комбинировать:
```
┌────────┬───────┬────────┐
│ A \ B  │ react │ static │   Виджет A является родителем виджета B
├────────┼───────┼────────┤
│ react  │   +   │   ±    │
│ static │   +   │   +    │
└────────┴───────┴────────┘

```

На данный момент не статичный корневой виджет ломает верстку (#45).
Стоит избегать не статичных виджетов внутри тега head, так как такие виджеты оборачиваются в div, что приводит к тому что браузер выбрасывает их в body

Со временем, будут реализованы и оставшиеся комбинации.

## Страницы

[ExamplePage](https://github.yandex-team.ru/market/marketfront/tree/master/market/src/widgets/pages.desktop/ExamplePage)

Виджетом верхнего уровня является виджет высшего порядка `widgets/core/Root`, принимающий на вход страничный виджет и некоторые настройки, которые определяются в роутах.

Сразу заметим, что `Root` сам определяет, какие ресурсы (js и css) подключить. Для этого используются манифесты: для enb (`desktop.bundles/manifest/index.js`) и webpack (`dist/browser/manifest.json`). На страницах, отличных от прогрессивных доступ к манифестам осуществляется следующим образом: `/.bundles.webpack.bundleName.js`.

Для создания новой страницы достаточно выполнить следующие шаги:

1. Создать роут с указанием `Progressive` страницы.
2. Создать страничный виджет в `widgets/pages`.
   (Для создания страничного виджета можно взять готовый, например, `ExamplePage`. Нужно скопировать содержимое каталога `/widgets/pages/ExamplePage` в каталог `/widgets/pages/TestPage`. Также нужно обновить поле name в файле `index.js`).
3. Выполнить сборку проекта соответствующими командами.

Пример роута для прогрессивной страницы:

```js
{
    name: 'market:example',
    pattern: '/example',
    data: {
        method: 'GET',
        pageName: 'Progressive',
        pageData: {
            pageWidget: 'ExamplePage',   // имя виджета в widgets/page
        },
    },
}
```

## Джобы

Рассмотрим общие джобы, определённые в `apiary-annex`.

### `titleJob`

Джоба для выставления `<title>`. Игнорируются все джобы от виджетов, не лежащих на main-пути. Первая джоба выставляется в блокирующем режиме, потом отложенно выставляется последняя.

```js
import {titleJob} from '@yandex-market/apiary-annex/jobs';

titleJob(Promise.resolve('some <title> content'))
titleJob(Promise.resolve(null)) // отменить выставление заголовка
```

### `metaJob`

Джоба для выставления метаинформации (`<meta>`). Результирующая мета получается смёрживанием всех джоб виджетов на main-пути. Метаинформация выставляется только при отдаче роботу.

```js
import {metaJob} from '@yandex-market/apiary-annex/jobs';

metaJob({
    type: Promise.resolve('website'),
    title: Promise.resolve('Гвозди'),
    description: Promise.resolve('Какие-то гвозди'),
    canonical: Promise.resolve(['somePageId', {...}])
    publishedTime: Promise.resolve(new Date('2017-08-24')),
    images: Promise.resolve(['//yastatic.net/market-export/_/i/market-icon.png']),
    prevPage: Promise.resolve(['somePageId', {...}]),
    nextPage: Promise.resolve(['somePageId', {...}]),
    robots: Promise.resolve({index: false, follow: true}),
})
```

### `cookieJob`

Джоба для выставления кук. Все куки выставляются в отложенном режиме, с клиента. Все куки, перечисленные в джобе выставляются атомарно.
Доступные опции см. в [jshttp/cookie](https://github.com/jshttp/cookie)

```js
import {cookiesJob} from '@yandex-market/apiary-annex/jobs';

cookiesJob({
    'some-cookie': Promise.resolve('1'),
    'another-cookie': Promise.resolve(['1', {maxAge: 24 * 60 * 60}]),
    'cancel': Promise.resolve(null), // отменить выставление куки
})
```

### `redirectJob`

Джоба для совершения редиректа. Выполняется редирект для последней выставленной джобы от виджета на main-пути.

```js
import {redirectJob} from '@yandex-market/apiary-annex/jobs';

redirectJob(Promise.resolve(['somePageId', {...}]))
redirectJob(Promise.resolve([['somePageId', {...}], 301])
redirectJob(Promise.resolve('url'))
redirectJob(Promise.resolve(['url', 301]))
redirectJob(Promise.resolve(null)) // не совершать редирект
```

### `statusJob`

Джоба для выставления статуса ответа. Выставляется последний статус от виджетов на main-пути. Выполняется только для роботов.

```js
import {statusJob} from '@yandex-market/apiary-annex/jobs';

statusJob(Promise.resolve(508))
statusJob(Promise.resolve(null)) // отменить выставление статуса
```

## Метрика

[Документация](https://github.yandex-team.ru/market/cia/blob/master/README.md)

Пакет [market/cia](https://github.yandex-team.ru/market/monomarket/tree/master/lib/lib/cia) содержит необходимые компоненты и хоки для работы с метрикой. Поддерживается как работа в виджетной системе, так и работа с обычным, redux-овым стором.

Здесь же ограничимся некоторыми замечаниями:

- Зоны именуются в camelCase
- Минимально кладём в данные зонам
- Зоны работают и в статичных виджетах
- Не стоит ради более красивой цели метрики сокращать имена экшенов

## Отладка

[Apiary Shower](https://github.yandex-team.ru/belirafon/apiary-page-viewer) – инструмент для анализа, просмотра и изучения композиции apiary-виджетов на html-странице.

![](resources/apiary-shower.png)

Для получения дополнительной отладочной информации, можно передавать специальные query-параметры при запросе. Например, `_mod=robot&_mod=+dump&_filter=/content/a`

- `_mod=robot`
Включает режим отдачи "как роботу". Появляется метаинформация, пропадает клиентская инициализация, вычисление и доставка патчей и bare-виджетов. Другими словами, отдаётся только вёрстка.

- `_mod=dump`
Отдаёт только дамп с различной полезной информацией. Для использования, имеет смысл поставить расширение браузера для форматирования json.

Все временные отметки в дампе считаются относительно начала запроса.

<details>
<summary>Пример вывода</summary>
<p>

![](resources/debug-dump.png)

</p>
</details>

- `_mod=+dump`
Даёт дамп, аналогичный моду `dump`, только в консоль. Циклические ссылки, если были, при этом восстанавливаются.

<details>
<summary>Пример вывода</summary>
<p>

![](resources/debug-dump-1.png)

</p>
</details>

- `_mod=timers`
Дампит клиентские таймеры в консоль.

<details>
<summary>Пример вывода</summary>
<p>

![](resources/debug-timers.png)

</p>
</details>

- `_mod=requests`
Дампит запросы ресурсов к бекендам.

<details>
<summary>Пример вывода</summary>
<p>

![](resources/dump-requests.png)

</p>
</details>

- `_mod=withMissmatch`
  Добавляет подсчет диффа для StateDivergence.

- `_filter=/some/id`
Оставляет на странице только виджет с указанным идентификатором, его родителей и детей. Стоит заметить, что другие виджеты часто тоже могут быть выполнены, хотя и не полностью.

Можно задавать несколько фильтров.

<details>
<summary>Пример вывода</summary>
<p>

![](resources/debug-filter.png)

</p>
</details>

## Обзор ошибок

Полный список ошибок с описанием:

* [Серверные](../src/server/errors.ts)
* [Клиентские](../src/client/errors.ts)

Рассмотрим наиболее частые системные ошибки:

- `UnfilledSlot` — попытка вставить во view слот, для которого в контроллере ничего не вставляется
- `BareSlotInView` — попытка отрендерить bare-слот
- `UnusedSlot` — в контроллере что-то вставлено в слот, однако во view он не заиспользовался
- `StateDivergence` — несколько виджетов пытаются положить в одну и ту же коллекцию разъехавшиеся данные. Чаще всего это означает, что данные недостаточно хорошо нормализованы или предметная область спроектирована неправильно (что так же стоит исправлять на этапе нормализации)
- `AsyncControllerIsForbidden` — попытка использовать `async`-контроллер или контроллер, возвращающий промис. Для использования асинхронных контроллеров необходимо указать директиву `asyncController`
