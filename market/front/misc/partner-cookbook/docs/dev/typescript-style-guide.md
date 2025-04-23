# Соглашения по работе с TypeScript

Вопросы по TypeScript-у можно задавать в общеяндексовый слак-канал [#community-typescript](https://yndx-market.slack.com/archives/C01J76S6GES).

---

- [Описание типов](#описание-типов)
- [Именование типов](#именование-типов)
- [Перечисления](#перечисления)
- [Ошибки типизации](#ошибки-типизации)
- [Написание тестов](#написание-тестов)
- [Использование хелперов](#использование-хелперов)
  - [Omit и Pick](#omit-и-pick)
- [Использование any](#использование-any)
- [Примеры](#примеры)
  - [React компонент](#react-компонент)
  - [High Order Component](#high-order-component)
  - [Резолвер](#резолвер)

## Описание типов

Типы в _TypeScript_ можно описывать с помощью алиасов (_type alias_) или интерфейсов (_interface_). Для поддержания кодовой базы в одном стиле типы нужно описывать с помощью алиасов.

```ts
// Так делать НЕ стоит ❌

interface Props {
  isDisabled: boolean;
}
```
```ts
// Так делать СТОИТ ✅

type Props = {
  isDisabled: boolean;
}
```

Интерфейсы можно использовать в случае расширения интерфейса внешней библиотеки ([_declaration merging_](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)), описания тайпингов для не типизированного кода или полиморфизма.

<details>
  <summary>Аргументация за использование алиасов</summary>
  <br/>
  
  - _Type alias_ по возможностям не уступают интерфейсам, поэтому нет разницы, что использовать, но имеет смысл для консистенции использовать что-то одно и алиасы позволяют union/intersection;
  - После миграции проекта с _Flow_ в коде все типы переведены на алиасы типов, поэтому сейчас в кодовой базе используются именно они. После _Flow_ алиасы будет намного привычнее;
  - У интерфейсов есть фича _declaration merging_ (paste.yandex-team.ru/3924489), которая может случайно привести к неявным расширениям интерфейса.

</details>


## Именование типов

Стоит использовать PascalCase-нотацию и не добавлять префиксы I и T. Если есть конфликт с классом или модулем, то можно добавить постфикс (например, Type).

```ts
// Так делать НЕ стоит ❌

interface BaseProps   // Не используем interface
type Baseprops        // Не отвечает требованию PascalCase-нотации
type IBaseProps       // Не используем префиксы
```
```ts
// Так делать СТОИТ ✅

type BaseProps
```

## Перечисления

В проекте запрещено использование Enum-ов (https://www.typescriptlang.org/docs/handbook/enums.html):

```ts
// Так делать НЕ стоит ❌
enum Direction {
  Up = 'UP',
  Down = 'DOWN',
}
```
```ts
// Так делать СТОИТ ✅
const DIRECTION = {
  UP: 'UP',
  DOWN: 'down',
} as const;
```

Если вам не нужна поддержка перечислений в рантайме, то можно (и нужно) использовать литеральные типы:

```ts
type Direction = 'UP' | 'DOWN';

function respond(direction: Direction) {
  // ...
}
```

<details>
  <summary>Аргументация против использования Enum</summary>
  <br/>
  
  - Генерирует boilerplate-код (одна из немногих фичей в TypeScript, которая прорастает в рантайм)
  - Фича, не имеющие аналогов в JavaScript (хотя `enum` является зарезервированным словом в стандарте)
</details>

## Ошибки типизации

Если TypeScript выдает ошибку компиляции, которую сложно исправить (например, неверные тайпинги внешней библиотеки или явная передача неверных переменных в тестах), то можно использовать явный кастинг внутри модуля (сохраняя типизированный интерфейс ввода/вывода) или расширить интерфейс через `declaration merging`.

Например, в примере ниже будет ошибка _Property 'dataset' does not exist on type 'EventTarget'_:

```ts
const onClickHandler = (event: React.MouseEvent<HTMLButtonElement>) => {
  const {name} = event.target.dataset;
                              ^^^^^^^   
  // ...
};    
```

Для ее исправления можно явно привести тип `target` к `HTMLButtonElement`:

```ts
const onClickHandler = (event: React.MouseEvent<HTMLButtonElement>) => {
  const {name} = (event.target as HTMLButtonElement).dataset;

  // ...
};
```

Если варианты выше не помогают, то можно использовать `@ts-expect-error` с описанием проблемы:

```ts
// Так делать НЕ стоит ❌

// @ts-ignore Возвращает неверный тип      // Не используем @ts-ignore
// @ts-expect-error                        // Не добавлен комментарий с проблемой
```
```ts
// Так делать СТОИТ ✅

// @ts-expect-error Возвращает неверный тип
```

`@ts-expect-error` **не надо** использовать в тестах, когда нет смысла описывать полное состояние или моки данных (см. ниже)

<details>
  <summary>Про @ts-ignore</summary>
  <br/>
  
  Комментарий `@ts-ignore` делает почти то же самое, что и `@ts-expect-error` - сообщает компилятору пропускать ошибки на следующей строке. Разница в том, что `@ts-ignore` ничего не сделает, если следующая строка не содержит ошибок ([пример](https://www.typescriptlang.org/play?#code/C4TwDgpgBACghgJwgO2FAvFAShAxgewQBMAeZAVwFsAjCBAGigGdgEBLZAcwD4BuAKAD0gqACEIACzgA3NoShsmUCAA84uYABsQUYBOhM4laB10TFUXHCYQhIgALAmAWjadkhW6EhiE+ANYoAIwYsIgowADaLOxcALoCwlCOLqqQGs50fgj83tCifoHIAEyh8Eio0awcnAn8QgBUUPwAqjaaEExKTq7unlC0mvgA7swcuAb4xtT4RDpwmkhwc1AAZmwqEERm0GB+1B2UAHRQAOoSOm4eSAqrO0gA5Er8HlB7+AcQlAD8-A2CdmSPSunly4GgADENlsQphyhFIhQaHQ6kkUpkVOlgJkENkwT4oZsiKU4eFKkjaAgEkA)). А `@ts-expect-error` сообщит, что комментарий бесполезен ("I'm useless"), поэтому верно типизированный код не будет игнорироваться компилятором. 
  
  Так же есть рекомендуемое правило в [typescript-eslint](https://github.com/typescript-eslint/typescript-eslint/blob/HEAD/packages/eslint-plugin/docs/rules/ban-ts-comment.md), которое запрещает использовать `@ts-ignore`.
  
</details>

## Написание тестов

Бывает ситуация, когда нет смысла описывать полное состояние или моки данных. В этих случая лучше всего далать так:
```ts
// Так делать НЕ надо ❌

// @ts-expect-error не хочу воспроизводить структуру
const context: Context = {
  params: {
    businessId: 1234,
  },
};

// @ts-expect-error не хочу воспроизводить структуру
const offerIdsInfo: OfferIdsInfo = {
  offerIds: [123, 456],
};

// @ts-expect-error не хочу передавать все аргументы
Header({isOfferListEmpty: false});
```
```ts
// Так делать надо ✅
import {mockType, createMockContext} from 'spec/jest';

const context: Context = createMockContext({
  params: {
    businessId: 1234,
  },
})

const offerIdsInfo: OfferIdsInfo = mockType({
  offerIds: [123, 456],
});

Header(mockType({isOfferListEmpty: false}));
```
При написании моков на функции мы иногда хотим узнать, сколько раз вызовется эта функция, с какими аргументами, etc...
Но typescript ничего не знает о том, что функция замокана, поэтому ему надо помочь:
```ts
// Так делать НЕ надо ❌

jest.mock('app/resolvers/shop', () => ({
  getShopManager: jest.fn(),
}));
// ...
// @ts-expect-error typescript ругается :(
getShopManager.mockReturnValue(123);
// @ts-expect-error typescript ругается :(
expect(getShopManager.mock.calls[0][1]).toBe(res.id);
```
```ts
// Так делать надо ✅
import {mocked} from 'ts-jest/utils';

jest.mock('app/resolvers/shop', () => ({
  getShopManager: jest.fn(),
}));
// ...

expect(mocked(getShopManager).mock.calls[0][1]).toBe(res.id);
mocked(getShopManager).mockReturnValue(123);
```

## Использование хелперов

В TypeScript есть много полезных хелперов, которые рекомендованы к использованию: https://www.typescriptlang.org/docs/handbook/utility-types.html

### Omit и Pick

#### Когда стоит использовать

Хороший кейс использования `Omit` и `Pick` - обертки над сущностью (пример, _HOC_ в React). Это может быть, к примеру, специализация компонентов из UI-кита.

```ts
function SpecializedComponent(props: Omit<React.ComponentProps<typeof Component>, 'myprop'>) {
  return <Component {...props} myprop={foo}>
}
```

В этом случае ts будет запрещать явно использовать проп в коде

```ts
<SpecializedComponent myprop={123} /> //error
```

#### Когда НЕ стоит использовать

Не стоит использовать `Pick`, `Omit` и `Intersection operator` (&) для переиспользования "похожих" объектов. Вместо этого копировать свойства объектов явно. Мотивация: при неаккуратном использовании это приводит к сильному связыванию типов из разных архитектурных слоёв. После этого оказывается, что добавление, например, колонки в таблицу БД приводит к изменению типа во вьюхе, хотя эти данные туда не передаются. Как итог, типы начинают врать. Вторая причина: отладка. Typescript не разворачивает такие типы, и в описании разработчик видит `Pick<Omit<A & B>, 'foo'>, 'bar'>`:

```ts
// Так делать НЕ стоит ❌

type UserInput = {
  login: string;
  password: string;
}
type UserModel = {
  id: string;
} & UserInput;

type UserResponse = Omit<UserModel, 'password'>;
```
```ts
// Так делать СТОИТ ✅

type UserInput = {
  login: string;
  password: string;
}

type UserModel = {
  id: string;
  login: string;
  password: string;
}

type UserResponse = {
  id: string;
  login: string;
}
```

Но в случае если тип напрямую зависит (наследуется) от другого, то использование Pick/Omit в приоритете.

## Использование any

Тип `any` **запрещен** к использованию, так как он сводит к нулю пользу _TypeScript_. Если объект неизвестного типа, то можно использовать `unknown`, если какая-то функция может принимать один из типов, то стоит использовать [дженерики](https://www.typescriptlang.org/docs/handbook/2/generics.html) или явный каст переменной (с помощью `as`).

```ts
// Так делать НЕ стоит ❌

function flatten(array: any[]): any[] { ... }
```
```ts
// Так делать СТОИТ ✅

type NestedArray<T = unknown> = T | NestedArray<T>[];

function flatten<T>(array: NestedArray<T>[]): T[] { ... }
```

## Примеры

### React компонент

#### Компонент на основе _React-hooks_

```ts
import React, {useCallback} from 'react'
import {useI18n} from '~/containers/withI18n';

type Props = {...};

export const MyComponent = (props: Props) => (
  const i18n = useI18n();
  const onDragEnd = useCallback(() => {...}, []);
    
  return (...);
);
```

#### Компонент с использованием _recompose_

```ts
import React from 'react'

type BaseProps = {...};
type EnhancedProps = {...};

const MyComponentBase = (props: BaseProps) => (
  return (...);
);

export {MyComponentBase as Base};

export const enhance: HOC<BaseProps, EnhancedProps> = compose(/* список хоков */);

export const MyComponent = enhance(MyComponentBase);
```

Если внешних пропов (EnhancedProps) нет, то можно не передавать второй аргумент (по умолчанию он будет равен типу `{}`):

```ts
export const enhance: HOC<BaseProps> = compose(/* список хоков */);
```

### High Order Component

В настоящее время вместо HOC-ов рекомендуется использовать React Hook-и (по этой причине многие библиотеки типа [recompose](https://github.com/acdlite/recompose) перестали обновляться и сейчас не рекомендуются к использованию). Хуки хорошо типизируются, автоматически выводят типы и не создают hoc-hell (про использование хуков подробнее в [./client.md#использование-react-hooks](https://github.yandex-team.ru/market/partner-cookbook/blob/master/docs/dev/client.md#%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-react-hooks).

Если все же есть необходимость написать HOC, то в их типизации поможет пост: https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb .

### Резолвер

Пример резолвера `updateNavigation`:

```ts
// shared/resolvers/mbiPartner/turboSettings/updateNavigation.ts

import {createResolver, unsafeResource} from '@yandex-market/mandrel/resolver';
import type {Context} from '@yandex-market/mandrel/context';

type Params = {...};
type Response = {...};

async function updateNavigationImpl(ctx: Context, params: Params): Promise<Response> {
    const [response] = await unsafeResource(ctx, 'mbiPartner.updateNavigation', params);

    return response;
}

export const updateNavigation = createResolver(updateNavigationImpl, {
    name: 'updateNavigation',
    remote: true,
});
```

Тип `updateNavigation` автоматически выведется как `(ctx: Context, params: Params): Promise<Response>` и не нужно явно прописывать его как `typeof updateNavigationImpl`.
