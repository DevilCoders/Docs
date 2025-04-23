[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/promise-helpers)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/promise-helpers) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/promise-helpers)](https://oko.yandex-team.ru/pkg/@yandex-market/promise-helpers)

## О библиотеке

Содержит функции-хэлперы для работы с нативными промисами. Используем чтобы не тащить Bluebird на клиент.

## Использование

* Чтобы использовать либу в проекте, `npm install @yandex-market/promise-helpers --save`

* Внутри ESM (ES6), поэтому можно импортировать как:

    `import {props, spread} from '@yandex-market/promise-helpers'`

    `const {props, spread} = require('@yandex-market/promise-helpers')`

* Доступны flow и ts декларации

## Доступные функции-хэлперы

#### `attempt()` (Альтернатива `Bluebird.try()`/`Bluebird.attempt()`)
````typescript
import {attempt} from 'promise-helpers';

const callback = () => 'Hello, world';
attempt(callback).then((str: string) => str); // => 'Hello, world'

// @ts-expect-error Из-за того, что typeof str === 'string'
attempt(callback).then((str: number) => str);
````

#### `props()` (Альтернатива `Bluebird.props()`)
````typescript
const obj = {
  firstPromise: 'Hello, world!',
  secondPromise: 42,
};

props(obj).then((resolvedObj: {
  firstPromise: string,
  secondPromise: number,
}) => resolvedObj); // => {firstPromise: 'lol', secondPromise: 'kek'}

// @ts-expect-error Из-за того, что typeof resolvedObj.secondPromise === 'number'
props(obj).then((resolvedObj: {
  firstPromise: string,
  secondPromise: string,
}) => resolvedObj);
````

#### `spread()` (Альтернатива `Bluebird.spread()`)
````typescript
import {spread} from 'promise-helpers'

spread([
  Promise.resolve('Hello, world!'),
  42,
  new Promise<string>(resolve => setTimeout(resolve, 100, 'Hello, world!')),
],
(res1, res2, res3) => {
  return [res1, res2, res3] as const;
}); // => Promise<readonly ['Hello, world!', 42, 'Hello, world!']>

spread([
     Promise.resolve('Hello, world!'),
     42,
     new Promise<string>(resolve => setTimeout(resolve, 100, 'Hello, world!')),
],
// @ts-expect-error Из-за того, что typeof res2 === 'number'
(res1: string, res2: string, res3: string) => { 
     return [res1, res2, res3];
});

````

## Отличия от Bluebird

* Отказались от `Bluebird.join()` в пользу функции `spread()` в целях более чистой типизации
* `Bluebird.promisify` в Node.js-коде меняем на нативный `util.promisify`
