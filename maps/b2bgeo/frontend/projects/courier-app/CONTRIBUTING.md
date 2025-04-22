# TypeScript

Typescript везде где не может определить тип данных, приписывает any по умолчанию. Из-за этого могут быть пропущены ошибки:

Плохо:

```
export default connect(
  state => state.company.id, // state - any
)(Drawer);
```

Хорошо:

```
export default connect(
  (state: RootState) => state.company.id, // state.company может быть null
)(Drawer);
```

Поэтому при написании кода желательно, проверять вручную что typescript понял ваши преобразования. В WebStorm: cmd + наведение на переменную, должен появится тултип с названием переменной и его типе.

## Компоненты

Желательно не дублировать описание возвращаемых значений селекторов и экшенов.

Плохо:

```
// типизация селекторов
interface OwnProps {
  routes: Array<Route>;
  token: string;
}
// типизация экшенов
interface Props extends OwnProps {
  updateOrders: () => void;
  routeSelected: (id: string) => void;
}
```

Хорошо:

```
// типизация селекторов
interface OwnProps {
  routes: ReturnType<typeof getRoutes>;
  token: ReturnType<typeof getApiToken>;
}
// типизация экшенов
interface Props extends OwnProps {
  updateOrders: typeof updateOrders;
  routeSelected: typeof routeSelected;
}
```

## Экшены

Желательно у любых функций четко определять входные и выходные типы данных. Иначе аргументы typescript будет считать за any.

Плохо:

```
type FetchCompanyAction = {
    type: string;
    companyId: number;
}

const fetchCompany = (companyId): FetchCompanyAction => {
    type: FETCH_COMPANY,
    companyId, // companyId - any, и мапается на number
}

fetchCompany("123") // НЕ будет возникать ошибка валидации
```

Хорошо:

```
const fetchCompany = (companyId: number): FetchCompanyAction => {
    type: FETCH_COMPANY,
    companyId, // companyId точно number
}

fetchCompany("123") // будет возникать ошибка валидации
```

## Саги

Все что возвращаете через yield становиться any. Поэтому нужно обязательно указывать тип полученных данных.

Плохо

```
let token = yield select(getApiToken); // token - any
```

Хорошо:

```
let token: ReturnType<typeof getApiToken> = yield select(getApiToken);
```

Плохо:

```
const data = yield predictOrdersEta(courier.id, ...); // data - any
```

Хорошо:

```
const data: APIPredictOrdersEta = yield predictOrdersEta(courier.id, ...);
```

## Селекторы

Желательно указывать, тип возвращаемых значений, чтобы быстрее локализовывать проблемы. Все как с экшенами.

Плохо:

```
const getCompany = (state: RootState) => state.company;
```

Хорошо:

```
const getCompany = (state: RootState): Company | null => state.company;
```

В createSelector тоже важно переиспользовать указанные типы данных:
Плохо:

```
const getDebugInfo = createSelector<
    RootState,
    Status | null, // можно забыть про null
    Ping | null, // и копипаста, как следствие всегда тяжело поддерживать
    ShortDebugInfo
>(
    getStatus,
    getPing,
    (status, ping) => ({ status, ping })
);
```

Хорошо:

```
const getDebugInfo = createSelector<
    RootState,
    ReturnType<typeof getStatus>,
    ReturnType<typeof getPing>,
    ShortDebugInfo
>(
    getStatus,
    getPing,
    (status, ping) => ({ status, ping })
);
```

## Редьюсеры и api

Желательно не путать те сущности которые получены через api, и те что в сторе приложения. Ибо, например, при замене типа поля в запросе, ошибки будут показываться в компонентах, селекторах и т.п., тяжело будет локализовать проблему. Если будут определены типы которые вы ждете в сторе, тогда typescript подскажет, что сущности не соответствуют, и нужно внести изменения в адаптер (преобразователь API сущностей, во внутренние).
