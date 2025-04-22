# @yandex-market/mbo-reatom-utils


## Установка

```bash
npm install @yandex-market/mbo-reatom-utils
```
## Функции

### createBooleanMapAtom / createBooleanStringMapAtom

createBooleanMapAtom создаёт атом с Record<number | string, boolean>

Пример использования
```typescript
import { createBooleanMapAtom } from '@yandex-market/mbo-reatom-utils';

const { MapAtom, TrulyIdsAtom, SetAction, SetSomeAction, ResetAction } = createBooleanMapAtom<string>('BooleanMapAtom');
const { MapAtom, TrulyIdsAtom, SetAction, SetSomeAction, ResetAction } = createBooleanMapAtom<number>('BooleanMapAtom', true);
```

В случае типа number для правильных типов в атоме TrulyIdsAtom необходимо задать второй не обязательный параметр numericIds в true,
иначе TrulyIdsAtom будет содержать массив строк

### createEntityAtom

Создают атом содержащий указанный тип. Значение атома полученного из createDefinedEntityAtom не может быть null.

Пример использования

```typescript
import { createEntityAtom } from '@yandex-market/mbo-reatom-utils';

const { Atom, SetAction } = createEntityAtom<boolean>('BooleanAtom', false);
const { } = createEntityAtom<string[]>('StringArrayAtom', []);
const { } = createEntityAtom<string[] | null>('NullableStringArrayAtom', null);
```

### createFetcher

Создаёт обвязку для запросов на бэк, содержит атомы для хранения значения и для хранения флага загрузки

```typescript
import { createFetcher } from '@yandex-market/mbo-reatom-utils';

const { DataAtom, LoadingAtom, LoadAction } = createFetcher<RequestType, DataType>(
  'FetcherAtom',
  async (request, store, setData) => {
    const api = store.getState(ApiAtom);

    const response = await api.suppliersController
      .list(request)
      .catch(error => store.dispatch(ErrorHandleAction(error)));

    if (response) {
      setData(response);
    }
  },
  {} // should be DataType
);
```

Если стартовое значение не нужно или нужно чтобы атом мог быть пустым DataType должен включать в себя null

Например

```typescript
import { createFetcher } from '@yandex-market/mbo-reatom-utils';

const { DataAtom, LoadingAtom, LoadAction } = createFetcher<RequestType, string[] | null>(
  'FetcherAtom',
  async (request, store, setData) => {
    const api = store.getState(ApiAtom);

    const response = await api.suppliersController
      .list(request)
      .catch(error => store.dispatch(ErrorHandleAction(error)));

    if (response) {
      setData(response);
    }
  },
  null
);
```

Так же есть вариации createMapFetcher для случаев когда одного булева значения не достаточно
и нужно использовать Record<number | string, boolean> для хранения состояния загрузки.

### createProcessor

Создаёт обвязку для запросов на бэк, содержит атом для хранения флага загрузки.
Полностью аналогичен createFetcher за исключением отсутствия атома для хранения данных.

```typescript
import { createProcessor } from '@yandex-market/mbo-reatom-utils';

const { ProcessingAtom, ProcessAction } = createProcessor<RequestType>(
  'FetcherAtom',
  async (request, store) => {
    const api = store.getState(ApiAtom);

    const response = await api.suppliersController
      .list(request)
      .catch(error => store.dispatch(ErrorHandleAction(error)));
  }
);
```
