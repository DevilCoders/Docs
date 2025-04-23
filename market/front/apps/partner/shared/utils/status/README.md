# Модуль для работы со статусами

Какую проблему решает:
- В приложении часто возникает необходимость для рендера данных в одном из трех состояний `pending`, `done` или `failed`.
- Для состояния `failed` необходимо хранить информацию об ошибке, чтобы потом можно было использовать ее для рендера более информативного сообщения.
- Иногда требуется хранить состояние для сущностей одного типа, но с разным набором параметров/идентификаторов
(например нужно уметь одновременно отобразить статус обновления нескольких заказов, у которых разный `orderId`).

Данный модуль:
- Содержит утилиты и типы для удобной работы с состояниями.
- Унифицирует подход для работы с состояниями.
- Позволяет организовать хранение состояний в любом месте в стейте.

Как правило, состояния нужно будет хранить или для всей страницы, или для пиджета.

## Константы

### STATUS
Реэкспорт [константы из b2b-core](https://a.yandex-team.ru/arcadia/market/front/libs/b2b-core/b2b-core/shared/types/status.ts) для более удобного использования.

```ts
import {STATUS} from 'shared/utils/status';

const status = STATUS.pending;
```


## Типы

### Status

Реэкспорт для [типа из b2b-core](https://a.yandex-team.ru/arcadia/market/front/libs/b2b-core/b2b-core/shared/types/status.ts) для более удобного использования.

```ts
import type {Status} from 'shared/utils/status';

const status: Status = 'pending';
```

### StatusEventFactory

Для описания всех возможных состояний необходимо реализовать следующий тип (например обновление информации о заказе).

```ts
type UpdateOrderEvent = {
    type: 'updateOrder';
    data:
    | {status: 'pending', error: null, orderId: number}
    | {status: 'done', error: null, orderId: number}
    | {status: 'failed', error: UpdateOrderError, orderId: number}
};
```

Чтобы упростить создание таких типов используйте специальный generic тип `StatusEventFactory`.

```ts
import type {StatusEventFactory} from 'shared/utils/status';

type UpdateOrderEvent = StatusEventFactory<'updateOrder', {orderId: number}, UpdateOrderError>;
```

Особенности реализации:
- Параметры события и информация об ошибке опциональны, для отсутствующих значений будут применятся дефолтные типы.
- Уникальность события определяет ее тип и ее параметры.
- Если для события не указаны параметры, то такое событие является `Singleton` событием.


```ts
import type {StatusEventFactory} from 'shared/utils/status';

type SomeStatusEvent1 = StatusEventFactory<'someStatusEvent'>;
type SomeStatusEvent2 = StatusEventFactory<'someStatusEvent', {}>;
type SomeStatusEvent3 = StatusEventFactory<'someStatusEvent', {}, unknown>;
```

Типы `SomeStatusEvent1`, `SomeStatusEvent2` и `SomeStatusEvent3` идентичны.

Для пустых параметров используйте специальный тип `StatusEventEmptyParams`.

```ts
import type {StatusEventFactory, StatusEventEmptyParams} from 'shared/utils/status';

type SomeStatusEvent1 = StatusEventFactory<'someStatusEvent', StatusEventEmptyParams, SomeError>;
type SomeStatusEvent2 = StatusEventFactory<'someStatusEvent', {}, SomeError>;
```

Типы `SomeStatusEvent1` и `SomeStatusEvent2` идентичны, но на тип `{}` ругается ESLint.


Примеры:

[Описание событий](https://a.yandex-team.ru/arcadia/market/front/apps/partner/shared/pages/BusinessOrders/types/statusEvent.ts) для "Единой страницы заказов".

### StatusEvent

Абстрактный тип данных, в основном используется в утилитах. Любой тип, созданный через `StatusEventFactory`, можно присвоить к типу `StatusEvent`.

```ts
import type {StatusEventFactory} from 'shared/utils/status';

type UpdateOrderEvent = StatusEventFactory<'updateOrder', {orderId: number}, UpdateOrderError>;

const updateOrderEvent: UpdateOrderEvent = {...};
const statusEvent: StatusEvent = updateOrderEvent;
```

В реальности нам не придется создавать объекты вида `StatusEvent`, для работы со статусами и стейтом используются специальные утилиты.

### StatusesState

Для описания объекта с информацией о событиях, для последующего их хранения в стейте, используется специальный generic тип `StatusesState`.

```ts
import type {StatusesState} from 'shared/utils/status';

// Все необходимые события мы описали ранее с помощью StatusEventFactory.
type PageStatusesState = StatusesState<GetBusinessOrdersEvent | GetShipmentOrdersEvent | UpdateOrderEvent | ...>;
```

Полученный тип используем для описания стейта страницы (или пиджета).
Можно использовать любую структуру, для которой вам потом будет удобно писать селекторы и редьюсеры.

```ts
type State = AnyAppState & {
    page: {
        ...
        statuses: PageStatusesState;
    }
}
```

На этом работа по описанию типов для событий завершена, тип стейта готов к использованию.

### GetStatusEventType, GetStatusEventData, GetStatusEventParams, GetStatusEventError

Утилитарные типы, скорее всего вам почти никогда не придется их использовать.
Их назначение описано в [файле с реализацией](https://a.yandex-team.ru/arcadia/market/front/apps/partner/shared/utils/status/types.ts).


## Утилиты

Для работы с объектом с информацией о событиях (`StatusesState`) используются специальные утилиты.

### setStatus

Данная утилита используется в редьюсерах, и позволяет устанавливать состояние для одного из статусов.

Совет. Создайте себе отдельный редьюсер для работы со статусами, чтобы собрать все изменения в одном месте.

```ts
import {handleActions} from 'rainbow-actions/immer';
import {setStatus} from 'shared/utils/status';

// Где-то выше мы описали события и стейт.
type UpdateOrderEvent = StatusEventFactory<'updateOrder', {orderId: number}, UpdateOrderError>;
type PageStatusesState = StatusesState<UpdateOrderEvent>;

// Редьюсер для работы с состояниями.
export const statuses = handleActions<PageStatusesState, Actions>({
    [updateOrder.init.type]: (state, {payload}) => {
        const {orderId} = payload;

        setStatus(state, 'updateOrder', 'pending', {orderId});
    },
    [updateOrder.done.type]: (state, {payload}) => {
        const {orderId} = payload;

        setStatus(state, 'updateOrder', 'done', {orderId});
    },
    [updateOrder.fail.type]: (state, {payload}) => {
        const {orderId, error} = payload;

        setStatus(state, 'updateOrder', 'failed', {orderId, error});
    },
    ...
);
```

Помимо ф-ии `setStatus` существуют удобные алиасы `setStatusPending`, `setStatusDone` и `setStatusFailed`.

Особенности реализации:
- Статусы событий одного типа сохраняются в стейте под уникальным ключем, который вичисляется как `eventType` + хэш от параметров конкретного события.
Статус события и объект ошибки в вычислении ключа не используются
([пример реального стейта со статусами](https://paste.yandex-team.ru/10255539) для "Единой страницы заказов").
- Все перечисленные ф-ии мутируют первый аргумент `state`, но за счет `immer` мы получаем то, что нам требуется.
- Ф-ии сделаны мутирующими, чтобы вы могли применять их последовательно, если в одном редьюсере вы хотите обновить сразу несколько статусов для разных событий.
- Если для события не существует параметров, то для установки статуса `pending` или `done` вы должны передавать пустой объект.
- Если для события описаны параметры, то в качестве объекта с параметры необходимо передавать `Exact` тип.
- Если для события не описан тип ошибки, он по умолчанию `unknown`, то вам все равно придется передать какое-либо значение.

```ts
// Где-то выше мы описали события и стейт.
type SomeStatusEvent1 = StatusEventFactory<'someStatusEvent1', {}>;
type SomeStatusEvent2 = StatusEventFactory<'someStatusEvent2', {}, {message: string}>;
type SomeStatusEvent3 = StatusEventFactory<'someStatusEvent3', {x: number}, {message: string; code: string}>;
type UpdateOrderEvent = StatusEventFactory<'updateOrder', {orderId: number}, UpdateOrderError>;

type PageStatusesState = StatusesState<SomeStatusEvent1 | SomeStatusEvent2 | SomeStatusEvent3 | UpdateOrderEvent>;

// Редьюсер для работы с состояниями.
export const statuses = handleActions<PageStatusesState, Actions>({
    [SOME_ACTION]: (state) => {
        // Обновление статусов события без параметров.
        setStatusPending(state, 'someStatusEvent1', {}); // Ok. У события нет параметров.
        setStatusDone(state, 'someStatusEvent1', {}); // Ok. У события нет параметров.
        setStatusFailed(state, 'someStatusEvent1', {error: 'message'}); // Ok. Можно указать любую ошибку.
        setStatusDone(state, 'someStatusEvent1', {error: 'message'}); // Error. Мы вызвали setStatusDone, в этом состоянии не может быть ошибки.

        // Обновление статусов события без параметров, но с определенным типом ошибки.
        setStatusDone(state, 'someStatusEvent2', {}); // Ok.
        setStatusFailed(state, 'someStatusEvent2', {}); // Error. Требуется указать ошибку.
        setStatusFailed(state, 'someStatusEvent2', {error: {message: 'message'}}); // Ok.
        setStatusFailed(state, 'someStatusEvent2', {error: {message: 'message', foo: 'bar'}}); // Ok. Для ошибок не обязательно чтобы тип был Exact.

        // Обновление статусов события с параметрами и с определенным типом ошибки.
        setStatusDone(state, 'someStatusEvent3', {x: 1}); // Ok.
        setStatusDone(state, 'someStatusEvent3', {x: 1, y: 2}); // Error. Требуется указать Exact тип для параметров.
        setStatusFailed(state, 'someStatusEvent3', {x: 1, error: {message: 'message', code: 404}}); // Ok.
        setStatusFailed(state, 'someStatusEvent3', {x: 1, y: 2, error: {message: 'message', code: 404}}); // Error. Требуется указать Exact тип для параметров.

        // Пример одного и того же типа события, но с разыми параметрами. В стейте будут хранится две разные записи, это разные события!
        setStatusDone(state, 'updateOrder', {orderId: 1}); // Ok.
        setStatusDone(state, 'updateOrder', {orderId: 2}); // Ok.
    },
...
);
```

Примеры:

[Редьюсеры на изменение статусов](https://a.yandex-team.ru/arcadia/market/front/apps/partner/client.next/pages/BusinessOrders/reducers/statuses/index.ts) для "Единой страницы заказов".

### getStatus

Аналогично `setStatus`, но используется для получения статуса события. Как правило используется в селекторах.

Совет. Создайте себе отдельный модуль с селекторами для работы со статусами, чтобы собрать всю работу со статусами в одном месте.

```ts
import type {Status} from 'shared/utils/status';
import {getStatus} from 'shared/utils/status';

// Где-то выше мы описали события и стейт страницы.
type SomeStatusEvent1 = StatusEventFactory<'someStatusEvent1', {}>;
type SomeStatusEvent2 = StatusEventFactory<'someStatusEvent2', {x: number}>;

// Пример получения статуса для события без параметров.
const selectSomeStatusEvent1Status = (state: State): Status | undefined => {
    const {statuses} = state.page;

    return getStatus(statuses, 'someStatusEvent1', {});
}

// Пример получения статуса для события с параметрами.
const selectSomeStatusEvent2Status = (x: number, state: State): Status | undefined => {
    const {statuses} = state.page;

    return getStatus(statuses, 'someStatusEvent2', {x});
}
```

На ф-ию распространяются теже ограничения на объекты параметров, что и для ф-ии `setStatus`:
- Объект с параметрами должен быть `Exact` типом.
- Если для события не определены параметры, то нужно передать пустой объект.


Примеры:

[Селекторы для получения статусов](https://a.yandex-team.ru/arcadia/market/front/apps/partner/client.next/pages/BusinessOrders/selectors/statuses.ts) для "Единой страницы заказов".

### getStatusEventData

Используется для получения полной информации по событию, а не только ее статуса.
С помощью этой ф-ии можно получить информацию о параметрах события, статусе и ошибке.

```ts
import type {Status} from 'shared/utils/status';
import {STATUS} from 'shared/utils/status';

// Где-то выше мы описали события и стейт страницы.
type UpdateOrderEvent = StatusEventFactory<'updateOrder', {orderId: number}, UpdateOrderError>;

// Получение статуса события.
const selectUpdateOrderEventData = (orderId: number, state: State): GetStatusEventData<UpdateOrderEvent> => {
    const {statuses} = state.page;

    return getStatusEventData(statuses, 'updateOrder', {orderId});
}

const statusEventData = selectUpdateOrderEventData(1, state);

// Статус события.
const status = statusEventData?.status; // Status | undefined

// Ошибка для события.
const error = statusEventData?.error; // UpdateOrderError | null | undefined

if (statusEventData && statusEventData.status === STATUS.done) {
    const error = statusEventData.error; // null
}

if (statusEventData && statusEventData.status === STATUS.failed) {
    const error = statusEventData.error; // UpdateOrderError
}

// Получение параметров события.
const orderId = statusEventData?.orderId // 1 | undefined

if (statusEventData) {
    const orderId = statusEventData.orderId // 1
}
```

## isStatusDone, isStatusPending, isStatusFailed

В ряде случаев использование специальных функций поможет сократить длину кода.

Все перечисленные функции являются [guard](https://www.typescriptlang.org/docs/handbook/advanced-types.html#user-defined-type-guards)-ами.

```ts
import {STATUS} from 'shared/utils/status';

if (status1 === STATUS.done && status2 === STATUS.done && status3 === STATUS.done) {
    console.log('Ура, все получилось!');
}
```

тоже что и

```ts
import {isStatusDone} from 'shared/utils/status';

if (isStatusDone(status1) && isStatusDone(status2) && isStatusDone(status3)) {
    console.log('Ура, все получилось!');
}
```

Можно передавать `null` или `undefined` в качестве значения для более удобного использования.

```ts
const selectSomeStatusEventStatus = (state: State): Status | undefined => {
    const {statuses} = state.page;

    return getStatus(statuses, 'someStatusEvent', {});
}

const status = selectSomeStatusEventStatus(state);

if (isStatusDone(status)) {
    ...
}
```
