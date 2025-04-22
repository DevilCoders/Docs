# Использование Typescript

Официальная документация: https://www.typescriptlang.org/docs/home.html

Основой codestyle для нашего проекта служит [общекарточный codestyle](https://github.com/ymaps/codestyle/blob/master/typescript.md), который мы дополняем своими, более строгими правилами:

## Приоритезация интерфейсов над типами

С помощью типов (type) описываем только то, что нельзя описать с помощью интерфейсов (interface).

**Хорошо:**

```ts
interface A {
    field: string;
}

type B = A | {otherField: string};
```

**Плохо:**

```ts
type A = {
    field: string;
};

type B = A | {otherField: string};
```

## Порядок объявлений типов/интерфейсов

Любой тип/интерфейс должен быть объявлен до его использования.

**Хорошо:**

```ts
interface A {
    name: string;
}

let a: A = {name: 'A'};
```

**Плохо:**

```ts
let a: A = {name: 'A'};

interface A {
    name: string;
}
```

## Порядок элементов внутри класса

Принят следующий порядок элементов:

-   static properties/methods
-   private/protected properties
-   public properties
-   constructor
-   public methods
-   private/protected methods

Исключения сделано для метода `render` внутри react component, его описываем в конце декларации. Подробнее смотрите в [шпаргалке по созданию react component](./react.md).

## Именования типов и интерфейсов

Интерфейсы и типы именуются как классы с использованием PascalCase, без добавления дополнительных префиксов и суфиксов.

**Хорошо:**

```ts
interface Person {
    name: string;
}
```

**Плохо:**

```ts
interface IPerson {
    name: string;
}
```

## Экспорты и импорты

Весь код должен быть написан после импортов и до экспортов.

**Хорошо:**

```ts
import Trailer from '...';
interface Person {
    name: string;
}
function someFn() {...}
export default someFn;
export {Person};
```

**Плохо:**

```ts
export interface Person {
    name: string;
}
import Trailer from '...';
export default someFn;
function someFn() {...}
```
