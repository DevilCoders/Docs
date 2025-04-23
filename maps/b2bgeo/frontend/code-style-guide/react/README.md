# React (представление)

<a name="react-3-0"></a><a name="3.0"></a>

- [3.0](#react-3-0) Иерархия папок компонентов

  для компонентов 2 папки: `layouts` (НЕ переиспользуемые компоненты: страницы, App и т.п.) и `components` (переиспользуемые: Button, Input и т.п.)

  Если компонент используется только в одном родительском (и нигде в других местах) нужно поместить его внутрь:

  ```ts
  ExpectedOrders |
    ExpectedOrders.ts |
    ExpectedOrders.css |
    FailedTimeWindow |
    FailedTimeWindow.ts |
    FailedTimeWindow.css;
  ```

<a name="react-3-1"></a><a name="3.1"></a>

- [3.1](#react-3-1) Извлекать кастомные хуки в папку `hooks`

  > Зачем? Компоненты станут менее громоздкими, у хуков будут самодокументирующие названия, так будет гораздо проще разобраться в компоненте и понять назначение хука.

  Если хук `нельзя` переиспользовать, то извлечь его в подпапку `hooks` в папке компонента.

  ```ts
  ExpectedOrders | ExpectedOrders.ts | ExpectedOrders.css | hooks | useYourHook.ts;
  ```

  Если хук `можно` переиспользовать, то извлечь его в подпапку `hooks` в папке `src`.

  ```ts
     src
      | @types
      | components
      | hooks
         | useYourHook.ts
  ```

<a name="react-3-2"></a><a name="3.2"></a>

- [3.2](#react-3-2) Не дублировать описание возвращаемых значений селекторов и экшенов

  Плохо:

  ```ts
  // типизация селекторов
  type OwnPropsT = {
    routes: Array<Route>;
    token: string;
  };
  // типизация экшенов
  type DispatchPropsT = {
    updateOrders: () => void;
    routeSelected: (id: string) => void;
  };
  ```

  Хорошо:

  ```ts
  // типизация селекторов
  type OwnPropsT = {
    routes: ReturnType<typeof getRoutes>;
    token: ReturnType<typeof getApiToken>;
  };
  // типизация экшенов
  type DispatchPropsT = {
    updateOrders: typeof updateOrders;
    routeSelected: typeof routeSelected;
  };
  ```

  В createSelector тоже важно переиспользовать указанные типы данных:
  Плохо:

  ```ts
  const getDebugInfo = createSelector<
    RootState,
    Status | null, // можно забыть про null
    Ping | null, // и копипаста, как следствие всегда тяжело поддерживать
    ShortDebugInfo
  >(getStatus, getPing, (status, ping) => ({ status, ping }));
  ```

  Хорошо:

  ```ts
  const getDebugInfo = createSelector<
    RootState,
    ReturnType<typeof getStatus>,
    ReturnType<typeof getPing>,
    ShortDebugInfo
  >(getStatus, getPing, (status, ping) => ({ status, ping }));
  ```

<a name="react-3-3"></a><a name="3.3"></a>

- [3.3](#react-3-3) React.memo, React.useMemo и React.useCallback используем только обоснованно (там где это сильно влияет на производительность)

<a name="react-3-4"></a><a name="3.4"></a>

- [3.4](#react-3-4) Если у компонента нет props - мемоизируем (React.memo).

<a name="react-3-5"></a><a name="3.5"></a>

- [3.5](#react-3-5) Импорт React частей

  Плохо:

  ```ts
  class User extends React.Component<Props, State> {
  ```

  Хорошо:

  ```ts
  import { Component } from 'react';

  class User extends Component<Props, State> {
  ```

<a name="react-3-6"></a><a name="3.6"></a>

- [3.6](#react-3-6) Желательно в классовых компонентах использовать PureComponent

<a name="react-3-7"></a><a name="3.7"></a>

- [3.7](#react-3-7) Не используем вместе с функциональными компонентами connect, вместо этого используем useSelector, useDispatch
  > Почему? connect создает компонент дополнительную обертку и нужно писать типизацию (то что падает в props)

<a name="react-3-8"></a><a name="3.8"></a>

- [3.8](#react-3-8) Для типизации props используем только типы (не интерфейсы)
  ```ts
  type StatePropsT = { temp: number; }; 
  type DispatchPropsT = { temp2: string; }; 
  type OwnPropsT = { temp2: string; };
  type PropsT = StatePropsT & DispatchPropsT & OwnPropsT; 
  ```
  <a name="react-3-9"></a><a name="3.9"></a>
- [3.9](#react-3-9) Новый код пишем с использованием style-guides
 
  Плохо:

  ```postcss
      .item {
          color: #fff;
          padding: 4px;
          font-size: 14px;
          font-weight: bold;
      }
  ```

  Хорошо:
 
  ```postcss
      .item {
          color: $sidebarItem;
          padding: $u;

          @mixin bodyText;
      }
  ```
  <a name="react-3-10"></a><a name="3.10"></a>
- [3.10](#react-3-10) Все затронутые в задаче файлы переводим на style-guide
  > Зачем? Сразу все переводить смысла нету, так как в этом нету продуктовой необходимости. Переводя по 1 компоненту мы постепенно войдем в новый дивный мир
