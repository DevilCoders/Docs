# Стиль написания кода на JavaScript и TypeScript

## Именование

### Терминология

- `camelCase` — стиль именования, в котором первое слово пишется в нижнем регистре, во всех последующих первый символ выделяется верхним регистром, а между словами разделители не ставятся
- `PascalCase` — стиль именования, в котором первые символы всех слов выделяются верхним регистром,
  а между словами разделители не ставятся
- `kebab-case` — стиль именования, в котором слова пишутся в нижнем регистре и разделены символом `-`
- `snake_case` — стиль именования, в котором слова пишутся в нижнем регистре и разделены символом `_`
- `SCREAMING_SNAKE_CASE` — стиль именования, в котором слова пишутся в верхнем регистре и разделены символом `_`

### Общие правила

**Инструменты проверки**: отсутствуют

Идентификаторы любых программных сущностей должны:

- Иметь настолько говорящие имена насколько это возможно
- Использовать только общеизвестные аббревиатуры и сокращения
- Состоять только из ASCII символов, цифр и, в редких случаях, `_` или `$`

```javascript
errorCount; // 👍Всё очевидно
submissionId; // 👍Сокращение Id известно любому разработчику
httpResponse; // 👍Все Web-разработчики знают аббревиатуру HTTP

a; // 👎 "a" ничего не говорит о содержимом
nErr; // 👎 Неоднозначная аббревиатура
nCompConns; // 👎 Неоднозначная аббревиатура
sbmsnId; // 👎 Сложно распознать какое слово сокращали
```

#### Аббревиатуры

«Общеизвестные» аббревиатуры — те аббревиатуры, которые сможет понять любой разработчик в компании.
Примерами могут быть `Tcp`, `Http`, `Dfs`, `Xml`. Если в вашем проекте есть список часто употребляемых аббревиатур, то их следует задокументировать в файле `README.md`.

### Названия файлов

**Инструменты проверки**: отсутствуют

Названия файлов с кодом на JavaScript и TypeScript должны быть в `camelCase`. Примеры:

```
stringUtils.ts
useResizeObserver.ts
answerStatus.ts
```

Файлы с тестами должны иметь уточняющее расширение `spec`:

```
stringUtils.spec.ts
useResizeObserver.spec.ts
```

Допустимо задавать другие специфичные для фреймворка/библиотеки уточняющие расширения:

```
app.module.ts
userProfiles.service.ts
accounts.controller.spec.ts
```

Для файлов с React компонентами используется `PascalCase`:

```
Checkbox.tsx
Checkbox.examples.tsx
TextInput.tsx
TextInput.spec.tsx
```

### Переменные

**Инструменты проверки**: правила [camelcase](https://github.com/eslint/eslint/blob/master/docs/rules/camelcase.md) (для JavaScript) и [@typescript-eslint/camelcase](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/camelcase.md) (для TypeScript) в ESLint

Для имён переменных используется `camelCase`.

```typescript
let changeableData = null;
const unchangeableData = [];
```

В некоторых случаях допустимо использовать однобуквенные имена **локальных** переменных `i`, `j`, `k`, `l`, `m`, `n`, а также `x`, `y`, `z`:

```typescript
for (let i = 0; i < m; i++) {
  for (let j = 0; j < n; j++) {
    // ... k
    // ... l
  }
}

const x = 1;
const y = 2;
const z = 3;
let point = [x, y, z];
```

### Константы

**Инструменты проверки**: отсутствуют

Именуются в `SCREAMING_SNAKE_CASE`. Константами считать переменные, которые содержат
иммутабельные данные:

```typescript
const POLLING_DELAY = 1000; // ms

const MEDIA_BREAKPOINTS = {
  mobile: '320px',
  tablet: '768px',
  desktop: '1140px',
} as const;
```

### Функции

**Инструменты проверки**: правила [camelcase](https://github.com/eslint/eslint/blob/master/docs/rules/camelcase.md) (для JavaScript) и [@typescript-eslint/camelcase](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/camelcase.md) (для TypeScript) в ESLint

Имена функций пишутся в `camelCase`.

```typescript
function doSomething(...things: any[]) {
  // ...
}

const doSomethingElse = (...things: any[]) => {
  // ...
};
```

### Массивы

**Инструменты проверки**: правило [@typescript-eslint/array-type](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/array-type.md) в ESLint

В TypeScript есть два способа описать тип массива:

```typescript
// 1
const x: Array<string> = ['a', 'b'];
const y: ReadonlyArray<string> = ['a', 'b'];
const a: Array<string | number> = ['a', 'b'];

// 2
const x: string[] = ['a', 'b'];
const y: readonly string[] = ['a', 'b'];
const a: (string | number)[] = ['a', 'b'];
```

Рекомендуется использовать второй вариант.

### Классы, поля и методы

**Инструменты проверки**: правила [new-cap](https://github.com/eslint/eslint/blob/master/docs/rules/new-cap.md) (для JavaScript) и [class-name-casing](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/class-name-casing.md) (для TypeScript) в ESLint

Для имён классов используется `PascalCase`, а для полей и методов – `camelCase`.

```typescript
class Employee {
  public data: string;
  private privateData: string;

  public doSomething(): void {}
}
```

### Псевдонимы типов (Type Aliases)

**Инструменты проверки**: отсутствуют

Пишутся без префиксов в `PascalCase`:

```typescript
type AnimateTimings = {
  duration: number;
  delay: number;
  easing: string | null;
};

type WithProperties<P> = {
  [property in keyof P]: P[property];
};

type MetadataEntry = ClassMetadata | InterfaceMetadata | FunctionMetadata | MetadataValue;
```

### Интерфейсы (Interfaces)

**Инструменты проверки**: правило [@typescript-eslint/interface-name-prefix](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/interface-name-prefix.md) в ESLint

Должны начинаться с префикса `I`:

```typescript
interface IDevToolsInterface {
  services: Set<AnyInterpreter>;
  register(service: AnyInterpreter): void;
  onRegister(listener: ServicesListener): void;
}
```

### Обобщённые типы (Generics)

**Инструменты проверки**: правило [@typescript-eslint/generic-type-naming](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/generic-type-naming.md) в ESLint

Параметры обобщённых типов должны начинаться с префикса `T` и удовлетворять регулярному выражению `'^T[A-Z][a-zA-Z]+$'`:

```typescript
function createModel<TTestContext, TContext>() {
  // ...
}

class TestModel<TTestContext, TContext> {
  // ...
}
```

### Перечисления (Enums)

**Инструменты проверки**: отсутствуют

При написании Enum используется `PascalCase`:

```typescript
enum Color {
  Red = '#f00',
}
```

## Рекомендации по написанию кода

### Константы

Желательно константы выносить на уровень модуля или делать их статическими полями классов:

```typescript
const POLLING_DELAY = 1000; // ms

function startNotificationsPolling() {
  setInterval(() => {
    // Do something
  }, POLLING_DELAY);
}
```

```typescript
import { get } from 'got';

class PassportClient {
  private static RETRIES_COUNT = 2;

  public async getUserAccounts() {
    return get('...', { retry: PassportClient.RETRIES_COUNT });
  }
}
```

### Null или Undefined

Тип `undefined` предназначен для того чтобы обозначить, что значение не проинициализировано.
Его явное использование в коде должно быть ограничено.

Тип `null` говорит об отсутствии объекта. Он должен использоваться в коде явно.

### Проверка на Null и Undefined

Для безопасной работы с Null и Undefined значениями нужно применять [Optional Chaining](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#optional-chaining) и [Nullish Coalescing Operator](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#nullish-coalescing).

### Interface или Type Alias

Интерфейсы и псевдонимы типов похожи. На данный момент документация и спецификация устарели и не отражают реальных отличий между ними. Наиболее актуальный разбор есть на [StackOverflow](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types).

Интерфейсы рекомендуется использовать когда нужно описать публичный интерфейс для классов:

```typescript
interface IDisposable {
  dispose();
}

class TextEditor implements IDisposable {
  public dispose() {
    // ...
  }
}
```

Для расширения интерфейсов используется ключевое слово `extends`:

```typescript
interface IRequest extends IncomingMessage {
  // ...
}
```

В остальных случаях, например для описания структуры объектов, нужно пользоваться псевдонимами типов:

```typescript
type ResponseData = { messages: string[] } | { code: string };

type ServerResponse = {
  isError: boolean;
  data: ResponseData;
};

type SiteSettingsProps = {
  domain: string;
};

type PageProps = {
  title: string;
  description: string;
} & SiteSettingsProps;
```

### Import и Export

Импорты разбиваются на группы:

1. Встроенные модули – модули встроенные в браузер или Node.js (`http`, `fs`, `net`, ...)
2. Сторонние модули – модули из библиотек установленных через npm и описанных в файле `package.json`
3. Импорты модулей из текущего пакета

Группы отделяются друг от друга пустой строкой. Импорты стилей, картинок, других типов ресурсов разбиты на такие же группы. Каждый тип ресурсов отделяется друг от друга пустой строкой. В рамках группы строки сортируются по источнику импорта в алфавитном порядке. Если в группе присутствуют относительные импорты, то первично порядок задаётся уровнем вложенности (по убыванию).

В конце, после всех импортов, должна быть пустая строка.

Примеры:

```typescript
import React, { useCallback, useState, FC } from 'react';
import { useDispatch } from 'react-redux';
import { withRouter, RouteComponentProps } from 'react-router';
import { useDebouncedCallback } from 'use-debounce';

import { cn } from '../../shared/classnames';
import { someConstant, SomeClass } from '../exampleModule';

import 'some-library/dist/example.css';

import '../global/example.css';
import styles from './example.module.css';

import firstIconUrl from 'some-library/dist/exampleIcon.svg';

import secondIconUrl from '../icons/exampleIcon.svg';
import thirdIconUrl from './exampleIcon.svg';

// Your code
```

```typescript
import fs from 'fs';
import path from 'path';

import { NextFunction, Request, Response } from 'express';

import { SomeService } from '../service';
import { ISomeInterface, SomeType } from './types';

// Your code
```

Ключевое слово `export` применяется непосредственно рядом с объявлением экспортируемой сущности, а не в конце файла.

Примеры:

```typescript
export type LinkProps = {
  theme?: LinkTheme;
  view?: 'lyceum';
  behavior?: LinkBehavior;
};

export type LinkThemeProps = Pick<LinkProps, 'theme'>;
export type LinkBehaviorProps = Pick<LinkProps, 'behavior'>;

export const EduLink = compose(
  withPseudo,
  withViewLyceum,
  composeU(withThemeNormal, withThemeGhost, withThemePseudo) as Composition<LinkThemeProps>,
  composeU(withBehaviorRouter, withBehaviorExternal) as Composition<LinkBehaviorProps>,
)(LinkBase);
```

Дефолтные экспорты в общем случае рекомендуется не использовать, объяснение причин можно прочитать в этом источнике — «[Avoid Export Default](https://basarat.gitbooks.io/typescript/content/docs/tips/defaultIsBad.html)».

Есть несколько исключений:

- Фреймворк требует дефолтного экспорта из файла. Наиболее известный пример – страницы в Next.js:

```typescript
import { NextPage } from 'next';

const IndexPage: NextPage = () => (
  // ...
)

export default IndexPage
```

- Вы хотите выполнить динамический импорт компонента и воспользоваться React Suspense API:

```typescript
import React, { FC } from 'react';

const SomeComponent = lazy(() => import('./SomeComponent');
```

Дефолтный экспорт из файла рекомендуется прописывать в конце.
