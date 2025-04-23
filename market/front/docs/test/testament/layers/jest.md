# JestLayer

Слой для синхронизации среды исполнения jest

## Методы cлоя

### Constructor
 `constructor(filename: string, jest: Jest)`

- `filename` - имя файла с тестом
- `jest` - глобальный объект jest

```js
const mirror = new Mirror(); // создать mirror
const jestLayer = new JestLayer(__filename, jest); // создать jest-слой
```
Или c помощью [хелпера](../helpers.md)

```js
mirror = await makeMirror({
    jest: { // это будет передано в конструктор
        testFilename: __filename,
        jestObject: jest,
    }
});
jestLayer = mirror.getLayer('jest');
```

### runCode
```
runCode<TArg extends any[], TResult>(
    code: (...args: TArg) => TResult,
    args: TArg,
    filename?: string,
    callOptions?: CallOptions
): Promise<CallResult<TResult>>
```

Запускает код в обоих процессах

- `code` - функция, которую нужно запустить
- `args?` - аргументы, которые будут переданы в функцию
- `filename?` - имя файла, которое будет отображаться в стек-трейсе
- `callOptions?` - опции
  запуска ([CallOptions](https://a.yandex-team.ru/arcadia/market/front/libs/testament/src/mirror/method.ts#L3))

Возвращает результат вызова функции в виде объекта, через который можно получить доступ к результату выполнения функции на клиенте или бекенде

```js
await jestLayer.runCode(() => {
    jest.doMock(
        'path/to/module',
        () => ({mocked: 'data'})
    );
}, []); // мокаем какой-то модуль в обоих процессах

const result = await jestLayer.runCode(() => {
   return require('path/to/module').mocked;
}, []); // вызываем его в обоих процессах

console.log(result.getClient()); // 'data'
console.log(result.getBakend()); // 'data'
```

> Обратите внимание, что действия в mirror выполняются с применением await. Это позволяет синхронизировать окончание
> выполнения действий в двух процессах.

> Обратите внимание, для передачи аргументов у `runCode` есть отдельный параметр. Замыканию работать не будут

❌ Неправильно:
```ts
const a = 1;
const b = 1;

const result = await jestLayer.runCode(() => {
    return a + b;
}, []);

// Uncaught ReferenceError: a is not defined
```

✅ Правильно:
```ts
const a = 1;
const b = 1;

const result = await jestLayer.runCode((a, b) => {
    return a + b;
}, [a, b]);

// 3
```

Все внешние переменные должны быть явно переданы в `runCode` в виде массива вторым аргументов

Все дело в том, что для IPC взаимодействия функция сначала преобразуется в строку и затем снова в фукнцию и получившаяся функция ничего не знает о ранее доступных ей переменных

### doMock
```
doMock(
    moduleName: string,
    moduleFactory: function,
    options?: MockOptions,
    callOptions?: CallOptions
):Promise<CallResult<void>>
```
Мокает модуль (запускает [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options) в обоих
процессах)

- `moduleName` - имя модуля (см. докментацию
  к [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options))
- `moduleFactory` - функция мока (см. докментацию
  к [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options))
- `options?` - опции (см. докментацию
  к [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options))
- `callOptions?` - опции
  запуска ([CallOptions](https://a.yandex-team.ru/arcadia/market/front/libs/testament/src/mirror/method.ts#L3))

```js
await jestLayer.doMock(
    '@self/platform/widgets/content/FinancialProduct',
    () => ({create: () => Promise.resolve(null)})
);

await jestLayer.doMock(
    '@self/root/src/resolvers/report/resolveProductInfo',
    () => jest.fn().mockResolvedValue(require('@self/platform/widgets/BaseWithResolver/__spec__/mocks').mock)
);
```

Если вам нужно пробросить какие-то данные в мок, не спешите оборачивать jest.doMock в jestLayer.runCode, вместо этого используйте специальный хеллпер

```ts
import {packFunction} from '@yandex-market/testament/mirror';

await jestLayer.doMock(
    '@self/root/src/resolvers/report/resolveProductInfo',
    packFunction((foo) => {
      return {
        foo,
          bar: 123,
          baz: 456
      }
    }, [foo])
);
```

### requireModule
```
requireModule(
    moduleName: string,
    callOptions?: CallOptions
): Promise<CallResult<any>>
```

Подключает модуль (вызывает `require` в обоих процессах)

- `moduleName` - имя модуля
- `callOptions?` - опции
  запуска ([CallOptions](https://a.yandex-team.ru/arcadia/market/front/libs/testament/src/mirror/method.ts#L3))

Возвращает объект, через который можно получить доступ к результату подключения модуля на клиенте или бекенде

> скорее всего, вам это не понадобится ;)

## Выполнение методом только на бекенде

Иногда необходимо выполнить какой-то метод только на бекенд-процеесе (например, для того, чтобы замокать резолвер).
Любой из описанных выше методом можно вызвать из свойства `backend` и тогда он будет вызван только в бекенд-процессе:

```ts
await jestLayer.backend.doMock('path/to/resolver', ()=> ...);
```
