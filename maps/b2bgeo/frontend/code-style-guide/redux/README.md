# Redux (логика)

<a name="common-2-0"></a><a name="2.0"></a>

- [2.0](#common-2-0) Типизировать все что возвращается из генераторов

  Все что возвращаете через yield становиться any. Поэтому нужно обязательно указывать тип полученных данных.

  Плохо:

  ```ts
  let token = yield select(getApiToken); // token - any
  ```

  Хорошо:

  ```ts
  let token: ReturnType<typeof getApiToken> = yield select(getApiToken);
  ```

  Плохо:

  ```ts
  const data = yield predictOrdersEta(courier.id, ...); // data - any
  ```

  Хорошо:

  ```ts
  const data: APIPredictOrdersEta = yield predictOrdersEta(courier.id, ...);
  ```

<a name="redux-2-1"></a><a name="2.1"></a>

- [2.1](#redux-2-1) Используем по возможности автогенерируемые типы для API

  > Чтобы не поддерживать вручную (автоматизировать синхронизацию), и во время замечать ошибки возникающие из-за изменений api

  мониторинг API https://yandex.ru/courier/api/v1/doc:
  https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/frontend/projects/courier-manager/src/@types/generated-monitoring-api.d.ts

  солвер API https://courier.yandex.ru/vrs/api/v1/doc-en:
  https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/frontend/projects/courier-manager/src/@types/generated-solver-api.d.ts

<a name="redux-2-2"></a><a name="2.2"></a>

- [2.2](#redux-2-2) В мемоизируемые части стора не храним Set, Map и т.п.
  > такие типы данных не персиститься просто https://github.com/rt2zz/redux-persist#transforms

<a name="redux-2-3"></a><a name="2.3"></a>

- [2.3](#redux-2-3) Стараемся НЕ строить длинные цепочки селекторов > Такие длинные цепочки трудночитаемы (приводит к необдуманному использованию разработчиками) и плохо покрываются unit-тестами

  Плохо:

  ```ts
  export const selectOrders = createSelector(
    selectOrderIds,
    selectOrderById,
    (orderIds, orderByIds): OrderT[] => {
        // ...
    },
  );

  export const selectFilteredOrders = createSelector(
    selectOrders,
    selectQueryFilter,
    (orders, queryFilter): OrderT[] => {
          // ...
    },
  );

  export const selectCourierFilteredOrders = createSelector(
    selectFilteredOrders,
    selectCourierId,
    (filteredOrders, courierId): OrderT[] => {
         // ...
    }
  );
  ```

  Хорошо:

  ```ts
  export const selectOrdersForDashboard = createSelector(
    selectOrderIds,
    selectOrderById,
    selectQueryFilter,
    selectCourierId,
    (orderIds, orderByIds, queryFilter, courierId): OrderT[] => {
          const filteredOrders = ...;
          const courierOrders = ....;
          return courierOrders;
    },
  );
  ```

  <a name="redux-2-4"></a><a name="2.4"></a>

- [2.4](#redux-2-4) Названия action.type должны начинаться с части стора, где лежит событие

  > Такой подход поможет точно избежать коллизии имен событий

  Плохо:

  ```ts
  export enum TypesEnum {
    CREATE_ORDER_REQUEST = 'CREATE_ORDER_REQUEST',
    CREATE_ORDER_SUCCESS = 'CREATE_ORDER_SUCCESS',
    CREATE_ORDER_FAILED = 'CREATE_ORDER_FAILED',
  }
  ```

  Хорошо:

  ```ts
  export enum TypesEnum {
    CREATE_ORDER_REQUEST = 'orders/CREATE_ORDER_REQUEST',
    CREATE_ORDER_SUCCESS = 'orders/CREATE_ORDER_SUCCESS',
    CREATE_ORDER_FAILED = 'orders/CREATE_ORDER_FAILED',
  }
  ```
