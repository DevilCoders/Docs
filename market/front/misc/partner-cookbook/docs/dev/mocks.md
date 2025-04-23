# Моки в ПИ

Иногда разработка с настоящим бекендом затруднена в силу некоторых причин, как то
- бекенд не работает в данный момент времени
- бекенд пока не готов и отвечает в лучшем случае заглушками
- данные/ситуацию сложно воспроизвести

или есть необходимость посмотреть, как та или иная страница выглядит в разных состояниях, а быстро подготовить/воспроизвести эти состояния на тестинге не получается,

то хочется вместо ответа бекенда подложить мок ответа и хотя бы как-то разрабатывать/смотреть.

## mockOrGetInitialState, mockOrGetResolver, mockOrGetValue, mockOrGetApiMethod

Все перечисленные функции `mockOrGet*` работают по одному принципу: на вход подаётся набор моков и целевая функция, и если
- запрос пришёл из внутренней сети
- в запросе есть кука `_mock`
- в куке `_mock` передано имя мока из заданного набора
- мок имеет или генерирует не-undefined значение

то вместо вызова целевой функции будет использован мок,
в противном случае будет вызвана целевая функция в обычном режиме.

Функции `mockOrGet*` НЕ предназначены для использования в АТ. В АТ для этих целей должен быть использован Кадавр!

### Описание моков

Моки добавляются в исходный код вручную и типизируются с помощью `Mocks` или `StaticMocks`.

Хранение моков в исходниках используется исключительно для целей типизации - если разработчик меняет тип значения, то TS подсветит, что нужно допилить и моки.

```typescript
// mocks.ts
import type {Mocks, MockGetterParams, StaticMocks} from 'b2b-core/shared/utils/mocks/mockOrGetValue';
import type {Data} from 'whatever';

// Перечисляем все возможные моки.
// {'имя-мока':  мок}.
export const mocks: Mocks<Data> = {
  // Обычные статичные моки.
  'простой ответ': {data: ['foo']},
  'все возможные варианты': {data: ['foo', 'bar', 'baz']},

  // Генерируемый в runtime мок.

  // ВАЖНО: нужно указать тип возвращаемого значения функции, чтобы сработала типизация!
  // Без этого TS почему-то не будет проверять, что функция возвращает Data!
  'динамический мок': ({ctx}: MockGetterParams): Data => {
    const ololo = getSoleParam(ctx, 'ololo');
    return {data: [ololo]};
  },
};

export const mocks: StaticMocks<Data> = {
  // Только статичные моки.
  'простой ответ': {data: ['foo']},
};
```

### mockOrGetInitialState

Функция `mockOrGetInitialState` предназначена для мокирования вызова `getInitialState`. Она отличается от остальных функций тем, что передаёт в `state` список доступных моков. Этот список будет отображаться во внутреннем тулбаре под кнопкой `M` для быстрого и удобного переключения между моками.

```typescript
import {createContext} from '@yandex-market/mandrel/context';

import {mockOrGetInitialState} from 'b2b-core/shared/utils/mocks/mockOrGetInitialState';

import {mocks} from 'somewhere';

import getInitialState from './getInitialState';

function HtmlSomePage(this: typeof HtmlPlatformPage) {
  const ctx = createContext(this);
  const initialState = mockOrGetInitialState(ctx, mocks, getInitialState);
  // или если надо передать параметры, то
  // ... mockOrGetInitialState(ctx, mocks, () => getInitialState(ctx, params));

  this.push(promiseToResponse(this.buildInitialState(initialState)), 'initialState');
}
```

### mockOrGetResolver

Функция `mockOrGetResolver` предназначена для мокирования резолверов. Она отличается от остальных функций типизацией, упрощающей её использование для резолверов.

```typescript
import {mockOrGetResolver} from 'b2b-core/shared/utils/mocks/mockOrGetResolver';

import type {Response} from 'whatever';

import {mocks} from './mocks';

type Params = {/* ... */};

const resolverImpl = async (ctx: Ctx, params: Params): Promise<Response> => {/* impl */};

export const resolver = createResolver(mockOrGetResolver(mocks, resolverImpl), {
  name: 'resolver',
  // rest resolver options
});
```

### mockOrGetApiMethod

Функция `mockOrGetApiMethod` предназначена для мокирования api-страниц (json). Она отличается от остальных функций тем, что она учитывает, что метод api-страницы должен возвращать `Response`, а не `Promise`. Функциональность, которая оборачивается с помощью этой функции, должна находится в метода api-страницы.

В mockOrGetApiMethod обязательно передавать именно `function`, а не стрелочную функцию, чтобы можно было подменить `this` в момент исполнения.

```typescript
import {mockOrGetApiMethod} from 'b2b-core/shared/utils/mocks/mockOrGetApiMethod';

import {mocks} from './mocks';

ApiYourPage.prototype.someMethod = mockOrGetApiMethod(mocks, function (this: typeof ApiYourPage) {
  /* impl */
});
```

### mockOrGetValue

Функция `mockOrGetValue` реализует базовую функциональность подстановки моков, используется внутри всех вышеперечисленных функциях и должна быть использована во всех остальных случаях.

```typescript
// resolver.ts
import type {mockOrGetValue} from 'b2b-core/shared/utils/mocks/mockOrGetValue';

import {mocks} from './mocks';
import type {Response} from '../whatever';

type Params = {/* ... */};

const customAsyncFuncImpl = async (ctx: Context, params: Params): Response => {/* impl */};

export const customAsyncFuncImpl: typeof customAsyncFuncImpl =
  (ctx, params) => mockOrGetValue(ctx, mocks, () => customAsyncFuncImpl(ctx, params));

```

## Сквозные моки между страницей/резолверами/api-страницами/etc

Иногда для полноценной работы с моками мало просто уметь подставить мок, например, для `getInitialState`, но нужно, например, уметь подставить одновременно с этим и мок для какого-то резолвера, который вызывается при инициализации страницы на клиенте. Подобную схему можно реализовать по-разному, но хорошо бы придерживаться единого подхода по построению таких схем.

Так как имя используемого мока лежит в куке, то получить имя мока может как сама страница (mockOrGetInitialState), так и любой вызываемый с клиента резолвер (mockOrGetResolver) или api-страница (mockOrGetApiMethod). То есть для реализации моков для пользовательского сценария нам нужно, чтобы используемые сущности (страница/резолвер/api-страница/etc) имели у себя мок с нужным единым именем.

Например, если мы открываем страницу с моком `foo`, то чтобы подложить мок для резолвера, который вызывается при инициализации страницы, нужно добавить мок с именем `foo` для этого резолвера. Но при этом знание о связи этих моков в рамках нашего сценария остаётся только у разработчика, который пишет код, а другим разработчикам, которые придут позже читать/модифицировать этот код, связь этих моков будет неочевидна. Чтобы подчеркнуть эту связь, лучше в имени мока указывать как можно больше информации, например, не `foo`, а `Страница качества для DBS - скрытые товары - картдиффы по доставке` - тогда при работе со списком моков резолвера/api-страницы сразу будет видно, что, во-первых, этот мок будет использован на странице качества в рамках некоторого пользовательского сценария, во-вторых, поиск имени мока по коду выдаст только те моки, который участвуют в этом пользовательском сценарии на этой странице.
