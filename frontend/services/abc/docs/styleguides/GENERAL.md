# Рекомендации для написания redux-модулей

Это черновой текст, который нужно улучшать и дополнять.

## Типы модулей

Нужно подумать над тем, надо ли писать название компонента/фичи в имени файла

- actions.ts
  - рутины и экшены
- api.ts
  - функции, отправляющие запрос и возвращающие промис
- parsers.ts
  - функции, принимающие ответ от ручек, и возвращающие данные в формате стора
  - функции, принимающие данные в формате стора и возвращающие в формате параметров ручек
- reducers.ts
  - редьюсеры ¯\\\_(ツ)_/¯
  - тут пишем тип, описывающий объединение типов из types.ts,
    чтобы сформировать тип для всех возможных пэйлоадов в handleActions.
    Если перейти к typesafe-actions, такого объединения кажется
    не нужно будет (но это не точно)
- sagas.ts
  - саги ¯\\\_(ツ)_/¯
- selectors.ts
  - селекторы ¯\\\_(ツ)_/¯
- types.ts
  - тут пишем все типы, которые используются более чем в одном файле.
    Пишем тут, потому что
    - типов может быть много, и они будут усложнять читаемость соседних модулей
    - не нужно думать, из какого файла экспортировать тип
  - типы, которые не экспортируются, можно писать локально:
    - интерфейс селектора можно положить рядом с селектором
    - смесь типов можно описать в месте использования, как
      `PayloadUnion` в редьюсерах

## Нейминг

### Рутины
Постфикс `...Routine` (`getHolidaysRoutine`)

### Экшены
произвольный, с глаголом

### Вызовы апи
Произвольный, с глаголом.
Когда уместно, с упоминанием метода в названии
- `getEntity` — ok
- `patchEntity` — ok, но может быть `updateEntity`
- `postEntity` — странно, это скорее `createEntity`

### Парсеры
- бэк2фронт: `parseEntity`
- фронт2бэк: `prepareEntity`

### Редьюсеры
Тип с объединением типов пэйлоадов — `PayloadUnion` (?)

### Саги
- вотчеры — `watch...` (`watchHolidaysGet`)
- собственно саги — `...Worker` (`getHolidaysWorker`)

### Селекторы
Префикс `select...` (`selectHolidays`)

### Типы
[Про типы подробно в TYPES.md](./TYPES.md)

## Коннект к стору

https://redux.js.org/recipes/usage-with-typescript#typing-the-connect-higher-order-component

Вычисляем тип пропсов из коннектнутого компонента, а не наоборот, потому что
так меньше писать => меньше мест для ошибки

```typescript
// ДА
import { connect, ConnectedProps } from "react-redux";

const MyComponent: FC<MyComponentProps> = props => {
    const {
        holidasys, // тут вычисленный тип
        loadHolidays, // тут вычисленный тип
        visible, // тут явный тип
    } = props;
};

const connector = connect(
    (store: MyStore) => ({
        holidays: store.duty.holidays,
    }),
    {
        loadHolidays: holidaysRoutine,
    }
);

type MyComponentReduxProps = ConnectedProps<typeof connector>;
type MyComponentProps = MyComponentReduxProps & {
    visible: boolean;
};

const MyComponentConnected = connector(MyComponent);
```

```typescript
// НЕТ
import { connect } from "react-redux";

const MyComponent: FC<MyComponentProps> = props => { ... };

type MyComponentStateProps = {
  holidays: string[]; // явный тип
};
type MyComponentDispatchProps = {
  loadHolidays: Function; // явный тип
};
type MyComponentProps = MyComponentStateProps & MyComponentDispatchProps & {
  visible: boolean; // явный тип
};

const mapStateToProps = (store: MyStore): MyComponentStateProps => ({
  holidays: store.duty.holidays,
});
const mapDispatchToProps: MyComponentDispatchProps = {
  loadHolidays,
};

const MyComponentConnected = connect(mapStateToProps, mapDispatchToProps)(MyComponent);
```

## Типирование реакт-компонентов
```typescript
// ДА
import React, { FC } from 'react';
const MyComponent: FC<MyComponentProps> = props => { ... };
```

```typescript
// НЕТ
import React, { ReactElement } from 'react';
const MyComponent = (props: MyComponentProps): ReactElement => { ... };
```

Почему:
1. Дженерик FC делает больше типизации, чем явная типизация аргумента
   и возвращаемого значения
2. Меньше кода, меньше импортов, меньше мест для ошибки
