# Общее

<a name="common-1-0"></a><a name="1.0"></a>

- [1.0](#common-1-0) Новый код пишем на TS! Во всех репозиториях.

  > Почему? В светлом будущем весь проект будет на TypeScript.

<a name="common-1-1"></a><a name="1.1"></a>

- [1.1](#common-1-1) Желательно чтобы каждая строчка делала одно действие

  > Почему? Проще читать и дебажить

  Плохо:

  ```ts
  const columnKey = preparedColumns.find((_, columnIndex) => columnIndex === index)?.key;
  ```

  Хорошо:

  ```ts
  const column = preparedColumns.find((_, columnIndex) => columnIndex === index);

  if (column?.key) {
    // ...
  }
  ```

<a name="common-1-2"></a><a name="1.2"></a>

- [1.2](#common-1-2) Стараемся разносить крупные файлы (>500 строк) на более компактные

<a name="common-1-3"></a><a name="1.3"></a>

- [1.3](#common-1-3) Можно использовать мутацию, но чтобы не сломать в другом месте

<a name="common-1-4"></a><a name="1.4"></a>

- [1.4](#common-1-4) Там где можно код должен быть производительней, на ревью договариваемся о читаемости

<a name="common-1.5"></a><a name="1.5"></a>

- [1.5](#common-1-5) Осуждаем использование Event.stopPropagation

  Плохо:

  ```ts
  handleClick = (event: Event) => {
    event.stopPropagation(); // bad
  };
  ```

<a name="common-1-6"></a><a name="1.6"></a>

- [1.6](#common-1-6) У любых функций четко определять входные и выходные типы данных. Иначе аргументы TypeScript будет считать за any.

  > Зачем? Чтобы быстрее локализовывать проблемы.

<a name="common-1-7"></a><a name="1.7"></a>

- [1.7](#common-1-7) Использование any

  > Зачем? Типизация с any бесполезна.

  Использование any осуждается, если необходимо его использовать где не успеваете писать полноценные типы можно использовать глобальный TODO тип:

  ```ts
  type TODO = any;
  ```

  https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/frontend/projects/courier-manager/src/@types/core.d.ts

<a name="common-1-8"></a><a name="1.8"></a>

- [1.8](#common-1-8) Нейминг констант и переменных

  По проекту стараемся использовать camelCase, а не snake_case (только в местах обработки бекендовых сущностей)

  1. булевы переменные начинаем с "to be...": isOpen, hasErrors;
  1. типы заканчиваются на "...T": OrderT, StateT, PropsT;
  1. интерфейсы заканчиваются на "...I": FormatterI, ParserI;
  1. енамы заканчиваются на "...Enum": RoutingModeEnum, OrderStateEnum;
  1. селекторы начинаются с "select...": selectDepot, selectUser;

<a name="common-1-9"></a><a name="1.9"></a>

- [1.9](#common-1-9) Комментарии

  **Комментарии в коде должны быть обязательно на английском**.

  И обязательно комментируем не логичные места в коде (хитрости)

  ```ts
  const estimate = result.status.estimate * MS_IN_SECOND; // python timestamp in seconds
  ```

<a name="common-1-10"></a><a name="1.10"></a>

- [1.10](#common-1-10) Волшебные числа и строки нужно выносить декларативно в константы.

  Плохо:

  ```ts
  const estimate = result.status.estimate * 1000;
  ```

  Хорошо:

  ```ts
  const MS_IN_SECOND = 1000;
  const estimate = result.status.estimate * MS_IN_SECOND;
  ```

<a name="common-1-11"></a><a name="1.11"></a>

- [1.11](#common-1-11) По возможности используем early exit:

  Плохо:

  ```ts
  openOrder = (order: OrderT): void => {
    if (order) {
      this.props.openModal(order);
    }
  };
  ```

  Хорошо:

  ```ts
  openOrder = (order: OrderT): void => {
    if (!order) {
      return;
    }

    this.props.openModal(order);
  };
  ```

<a name="common-1-12"></a><a name="1.12"></a>

- [1.12](#common-1-12) Тернарники используем только там где НЕ вредит читаемости

  Плохо:

  ```ts
  reboundMapToMatches(zoom, isEmpty(points) ? [depotPoint] : points, isAfterClick);
  ```

  > тут не видно сразу сколько передано аргументов, тяжело читать, надо вглядываться в череду "?" ":" "," то есть строка сложная для быстрого восприятия

  Хорошо:

  ```ts
  const boundedPoints = isEmpty(points) ? [depotPoint] : points;
  reboundMapToMatches(zoom, boundedPoints, isAfterClick);
  ```

<a name="common-1-13"></a><a name="1.13"></a>

- [1.13](#common-1-13) НЕ используем вложенные тернарные операторы

  Плохо:

  ```ts
  const foo = maybe1 > maybe2
    ? "bar"
    : value1 > value2 ? "baz" : null;

  // split into 2 separated ternary expressions
  const maybeNull = value1 > value2 ? 'baz' : null;
  ```

  Хорошо:

  ```ts
  // split into 2 separated ternary expressions
  const maybeNull = value1 > value2 ? 'baz' : null;

  // better
  const foo = maybe1 > maybe2
    ? 'bar'
    : maybeNull;

  const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
  ```

  <a name="common-1-14"></a><a name="1.14"></a>

- [1.14](#common-1-14) По максимуму используем lodash

<a name="common-1-15"></a><a name="1.15"></a>

- [1.15](#common-1-15) Импортируем lodash, date-fns и т.п. модульно

  Плохо:

  ```ts
  import _ from 'lodash';

  _.random(0, 10);
  ```

  Хорошо:

  ```ts
  import random from 'lodash/random';

  random(0, 10);
  ```

<a name="common-1-16"></a><a name="1.16"></a>

- [1.16](#common-1-16) Если импортируем lodash/fp обязателен postfix Fp

  Плохо:

  ```ts
  import get from 'lodash/fp/get';
  ```

  Хорошо:

  ```ts
  import getFp from 'lodash/fp/get';
  ```

<a name="common-1-17"></a><a name="1.17"></a>

- [1.17](#common-1-17) Вместе c @ts-ignore пишем обязательно причину

  Плохо:

  ```typescript
      // @ts-ignore
      collect: ({ internalMonitor }) => ({
  ```

  Хорошо:

  ```typescript
      // @ts-ignore internalMonitor is private field  DropTargetMonitor
      collect: ({ internalMonitor }) => ({
  ```

  <a name="common-1-18"></a><a name="1.18"></a>

- [1.18](#common-1-17) При большом количестве параметров (>3) используем named parameters вместо positional parameters https://exploringjs.com/impatient-js/ch_callables.html#named-parameters

  Плохо:

  ```typescript
     const formatRouteLocation = (
        location: APILocation,
        locationIndex: number,
        allLocations: Array<APILocation>,
        routeIndex: number,
        vehicleRef?: string,
     ): PointT => {...}
  ```

  Хорошо:

  ```typescript
       const formatRouteLocation = ({
        location,
        locationIndex,
        allLocations,
        routeIndex,
        vehicleRef,
     }: LocationT): PointT => {...}
  ```

<a name="common-1-19"></a><a name="1.19"></a>

- [1.19](#common-1-19) Не строим логику полагаясь на выброс ошибок

  try ... catch не нравится:

  - работает не линейно, надо искать catch обертку выше;
  - нужно везде не забывать про обработку ошибок, оборачивать в try catch;
  - хочется снижать количество try ... catch блоков;
  - typescript: в catch error всегда any, код плохо типизируется;

  Плохо:

  ```typescript
     try {
        const response = yield api.getCourierTrack(..);
        // ...
     } catch (error) {
        yield put(getCourierTrackPartFail(error));
     }
  ```

  Хорошо:

  ```typescript
     const [error, response] = yield api.getCourierTrack(..)
     if (error !== null) {
        yield put(getCourierTrackPartFail(error));
     }
  ```

<a name="common-1-20"></a><a name="1.20"></a>

- [1.20](#common-1-20) При импорте общих иконок проставляем размеры иконки 100% и цвет заливки/обводки "currentColor"

  Так иконка будет адаптивной и легко переиспользуемой. Размеры можно будет задавать через родительский блок, а цвет через css свойство "color"

  Плохо:

  ```svg
     <svg width="16" height="16" viewBox="0 0 16 16" fill="#d93412">
     </svg>
  ```

  Хорошо:

  ```svg
     <svg width="100%" height="100%" viewBox="0 0 16 16" fill="currentColor">
     </svg>
  ```

<a name="common-1-21"></a><a name="1.21"></a>

- [1.21](#common-1-21) При приведении типов используем более явные конструкции

  Более явное приведение типов улучшает читаемость кода, особенно при увеличении кодовой базы

  Плохо:

  ```js
  const number = +count;
  const string = '' + id;
  const bool = !!value;
  ```

  Хорошо:

  ```js
  const number = Number(count); // parseInt etc..
  const string = String(id);
  const string2 = id.toString();
  const bool = Boolean(value);
  ```

<a name="common-1-22"></a><a name="1.22"></a>

- [1.22](#common-1-22) Именуем файлы с помощью kebab-case

  Сейчас в проекте встречаются два варианта наименований, camelCase и kebab-case, нужно придерживаться одного стиля

  Плохо:

  ```
    someFilename.ts
    someFilename.test.ts
  ```

  Хорошо:

  ```
    some-filename.ts
    some-filename.test.ts
  ```

<a name="common-1-23"></a><a name="1.23"></a>

- [1.23](#common-1-23) Не используем as

  В новом коде должно быть обоснованное ипользование `as`
  А если уже спустя пол часа ваших усилий это не убрать, то
  * Пишем причину, почему это осталось
  * Пишем тесты на это место

  Плохо:

  ```ts
    type RowWithIdT = {
      id: stirng;
    }

    type RowWithNumberT = {
      number: string;
    }

    type TableRowT = RowWithIdT | RowWithNumberT;

    handleChange((row as RowWithIdT).id)
  ```

  Хорошо:

  ```ts
    type RowWithIdT = {
      id: stirng;
    }
    type RowWithNumberT = {
      number: string;
    }

    type TableRowT = RowWithIdT | RowWithNumberT;

    const isRowWithId = (row: TableRowT): row is RowWithIdT => {
      ...
    }

    if (isRowWithId(row)) {
      handleChange(row.id)
    }
  ```

- [1.24](#common-1-24) URL'ы НЕ должны заканчиваться на "/"

    Почему имеено так?
    * Если везде будет разный стиль формирования урлов, будут проблемы с их конкатенацией (будут возникать двойные слеши, либо где-то пропадать)
    * При конкатенации легче добавить "/", чем писать код по его удалению;

    Плохо:

      ```ts
        const basepath = "https://yandex.com/";
        const url = "api/v1/depots";
      ```

    Хорошо:

      ```ts
        const basepath = "https://yandex.com";
        const url = "/api/v1/depots";
      ```
