# redux-saga-routines

Используем [redux-saga-routines](https://github.com/afitiskin/redux-saga-routines)

Для каждой рутины создается 5 actions и 5 action creators

`TRIGGER` → `REQUEST` → `SUCCESS` / `FAILURE` → `FULFILL`

### Action creators и их использование

* `routine.trigger()` - используем в компонентах, чтобы сделать запрос
* `routine.request() или routine.request(id)` - вызываем перед запросом в саге, выставляется `loading:true` в `loadingReducer`, 
`error: null` в `errorReducer`
* `routine.success(payload) или routine.success(id, payload)` - вызываем, когда успешно пришел результат, чтобы положить `payload`
* `routine.failure(error) или routine.failure(id, error)` - вызываем, когда запрос вернулся с ошибкой, 
выставляется ошибка в `errorReducer`
* `routine.fulfill()` - вызываем в finally саги, выставляется `loading: false` в `loadingReducer`

### Префикс

Префикс идентификатора экшена может быть любым, единственное требование — уникальность внутри стора.

### Использование

Создание рутины

```js
const prefix = 'abc-www/abc/feature/component';

const exampleRoutine = createRoutine(`${prefix}/example`);
```

* Используем actions, как `exampleRoutine.TRIGGER`, `exampleRoutine.SUCCESS`... 
* Используем action creators, как `exampleRoutine.trigger(payload)`, `exampleRoutine.success(payload)`...
* Префикс доступен в поле `exampleRoutine._PREFIX`

### Loading и error

Loading и error обрабатываются в отдельных редьюсерах, писать отдельно код для обработки
состояний загрузки и ошибки не нужно. Состояния кладутся в loadingReducer и errorReducer по префиксу рутины:
* `abc-www/Feature/Component/example/REQUEST`:
  * `{ "abc-www/Feature/Component/example": true }`
  * `{ "abc-www/Feature/Component/example": new Error(...) }`

Если один экшен отвечает за загрузку множества сущностей, состояния записываются по id
(код вызова экшена конечно нерабочий, просто для иллюстрации):
* `doAction("abc-www/Feature/PATCH_ENTITY/REQUEST")(id)`:
  * `{ "abc-www/Feature/PATCH_ENTITY": { [id]: true } }`
  * `{ "abc-www/Feature/PATCH_ENTITY": { [id]: new Error(...) } }`

Код редьюсеров лежит в [common/redux/common.reducers.ts](src/common/redux/common.reducers.ts).

### Получние данных о состояниях

Используй селекторы `selectIsLoading` и `selectError`, которые лежат
в [common/redux/common.selectors.ts](src/common/redux/common.selectors.ts).

```js
import { exampleRoutine, exampleRoutineWithIDs } from '...';
import { selectIsLoading, selectError } from 'common/redux/common.selectors';

const isExampleLoading = selectIsLoading(state, exampleRoutine._PREFIX); // => true | false
const hasExampleError = selectError(state, exampleRoutine._PREFIX); // => Error | null

const isExampleEntityLoading = selectIsLoading(state, exampleRoutineWithIDs._PREFIX, 42); // => true | false
const hasExampleEntityError = selectError(state, exampleRoutineWithIDs._PREFIX, 42); // => Error | null
```


### Дописывание редьсеров

Подразумевается, что редьюсеры для экшенов `TRIGGER`, `REQUEST`, `FAILURE`, `FULFILL` не пишутся.
Но их можно дописать, если нужны какие-то дополнения.

* для `TRIGGER` мы обычно вообще не пишем редьюсера
* для `REQUEST` автоматически выставляется `loading:true` и `error: null`
* для `FAILURE` автоматически выставляется `error`
* для `FULFILL` автоматически выставляется `loading: false`

`SUCCESS` нужно дописать в редьюсере фичи

### Разложение по id

Если нужно складывать в redux по id, то нужно дописать `complexMetaCreator`,
чтобы `loadingReducer` и `errorReducer` поняли, что нужно положить по id.
А также payloadCreator, чтобы id не было payload.

```js
const prefix = 'abc-www/feature/component';

const payloadCreator = {
    success: (id, payload) => (payload),
    failure: (id, payload) => (payload),
};

const complexMetaCreator = {
  request: (id) => ({ id, needDictionary: true }),
  failure: (id) => ({ id, needDictionary: true }),
  fulfill: (id) => ({ id, needDictionary: true }),
};

const exampleRoutine =  createRoutine(`${prefix}/example`, payloadCreator, complexMetaCreator);
```
