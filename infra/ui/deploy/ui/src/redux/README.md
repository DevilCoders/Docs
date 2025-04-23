# Хранилище Redux

Используется [redux-toolkit](https://redux-toolkit.js.org/), части хранилища организуются по срезам

Все срезы собираются в корне хранилища `./store.ts`

## Импорты
Так как redux — глобальное хранилище, многие компоненты используют его опосредованно через хуки.
Но сам редакс может подключать внешние slices, которые могут импортироваться через общую точку **/index.ts, и тащить за собой компоненты, которые используют редакс.
Так возникает циклическая зависимость в коде.
Чтобы этого избежать, для проблемных срезов импорты не используют файлы index.ts, вместо этого прописывается прямой путь до файла с описанием slice.
Так как в таких файлах нет тразитивных связей к компонентам, циклических зависимостей не возникает.

### RootState
Чтобы не было аналогичных проблем при импорте RootState, следует для него использовать `import type {RootState} from ...`


## Redux toolkit
Документация https://redux-toolkit.js.org/

Наиболее полезные методы апи описаны ниже

Срезы создаются функцией [createSlice](https://redux-toolkit.js.org/api/createSlice)
```typescript
createSlice({
   name: ..., // уникальное имя
   initialState: ..., // начальное состояние

   // явные действия
   reducers: {
      ...
   },

   // перехват любых событий
   extraReducers: {
      ...
   },
   // то же, но функцией c builder, предпочитаемый вариант для автовывода типов
   extraReducers: builder => {
      ...
   },
});
```

Для нормализации и `crud` операций предпочтительно использовать [createEntityAdapter](https://redux-toolkit.js.org/api/createEntityAdapter) при создании части хранилища

пример
```typescript
export const networkErrorAdapter = createEntityAdapter<NetworkError>({ // тип хранимых значений
   selectId: item => item.requestId, // откуда брать id
   sortComparer: (a, b) => sortHandler(a.requestId, b.requestId), // сортировка по умолчанию
});
```

Для формирования селекторов используется [createSelector](https://redux-toolkit.js.org/api/createSelector) в redux toolkit он проикдывается из `reselect`


## Вложенные срезы
### Создание
Вложенные срезы создаются как и обычные, но подключаются не к корню, а к целевому срезу.
Подключение происходит с помощью функции `getNestedSliceData`

```typescript
const { initialState, setupMatcher } = getNestedSliceData(
   namespace, // имя родительского среза
   // вложенные срезы
   {
      // полное уникальное имя у exampleSlice должно заканчиваться на /example
      // это необходимо, чтобы нужные события пробрасывались в нужные срезы

      // проверка имён добавлена на уровне типов
      example: exampleSlice,
      ...
   }
);

export type State = typeof initialState; // тип среза

export const slice = createSlice({
   name: namespace,
   initialState,
   reducers: {},
   extraReducers: builder => {
      setupMatcher(builder); // проброс событий во вложенные срезы

      // здесь также можно добавлять и другие события, если потребуется
   },
});
```

### Имена
Чтобы гарантировать уникальное имя, вложенному срезу задаются имя с `getNestedSliceName`

пример
```typescript
const name = 'quota';
const namespace = getNestedSliceName(ypReduxNamespace, name);
```

так как `ypReduxNamespace` и `name` константы, то и `namespace` будет константой, это используется в проверке типов при подключении к родительскому срезу.

### Селектор
Чтобы получить селектор вложенного среза без необходимости записывать всю цепочку префиксов, используется функция `getNestedSliceSelector`

пример
```typescript
export const selectQuotaStore = getNestedSliceSelector({
   name,
   initialState,
   parentSelector: selectYp,
});
```

## Асинхронные действия

`createAsyncThunk` возвращает обертку над асинхронными операциями

пример
```typescript
// аргументы итогового санка fetchTicketSummary
interface FetchTicketSummaryInput {
   id: string;
   startrekApi?: StartrekApi;
}

// результат, что будет в action.payload у события, далее прорастёт в редьюсеры
interface FetchTicketSummaryOutput {
   id: string;
   summary: string;
}

export const fetchTicketSummary = createAsyncThunk<FetchTicketSummaryOutput, FetchTicketSummaryInput>(
   'startrek/fetchTicketSummary', // уникальное имя
   // промис над FetchTicketSummaryOutput
   ({ startrekApi, id }) =>
      (startrekApi ?? getStarTrekApi())
         .getTicketSummary(id)
         .toPromise()
         .then(summary => ({ id, summary })),
);
```

Второй аргумент `createAsyncThunk` должен возвращать промис над ответом, имейте в виду при использовании `rxjs` как на примере выше.

### Генератор санков
Чтобы не писать каждый раз для каждой ручки апи обертки, можно само апи обернуть в генератор санков.
Далее Апи это объект, методы которого дергают ручки в сети и возвращают [Observable](https://rxjs.dev/guide/observable) над ответом.

Генератор `createRequestThunkGenerator` не только убирает лишний код, но и добавляет контроль сети и отсылку ошибок в Error booster.

На примерах:

Обёртка над `ypApi`
```typescript
export const ypRequestAsyncThunk = createRequestThunkGenerator(() => ypApi);
```
Здесь `ypRequestAsyncThunk` как и `createAsyncThunk` будет создавать санк, но принимает другие аргументы

```typescript
// задаём уникальное имя санка и имя метода из апи
const fetchPods = ypRequestAsyncThunk(`${namespace}/fetch`, 'getPods');

// вызов в компоненте
fetchPods
   // ключ запроса для контроля сети
   .withRequestKey('status.pods')
   // параметры метода getPods один в один
   ({podSetId: 'id-1', location: 'sas'})
;
```

В `payload` события записывается объект следующего типа
```typescript
interface ApiThunkOutput<Input, Output, Meta> {
   response: Output;
   params: Input;
   meta: Meta;
}
```

В редьюсере типы автоматически выводятся
```typescript
builder.addCase(fetchPods.fulfilled, (state, action) => {
   // всегда имеет тип ApiThunkOutput c нужными полями
   const { params, response } = action.payload;
   const { podSetId = '', location, limit, page, filter = '' } = params[0]; // первый аргумент метода ypApi.getPods
   const pods = response.values; // результат уже без обёртки Observable

   // ...
});
```

То же с явным указанием типов
```typescript
{
   [fetchPods.fulfilled.toString()](state, action: PayloadAction<GetApiThunkOutput<typeof fetchPods>>) {
      // всегда имеет тип ApiThunkOutput c нужными полями
      const { params, response } = action.payload;
      const { podSetId = '', location, limit, page, filter = '' } = params[0]; // первый аргумент метода ypApi.getPods
      const pods = response.values; // результат уже без обёртки Observable

      // ...
   }
}
```

