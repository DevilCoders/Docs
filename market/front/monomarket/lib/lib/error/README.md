[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/error)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/error) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/error)](https://oko.yandex-team.ru/pkg/@yandex-market/error)

# error

Модуль, экспортирующий базовый класс ошибок, наследующий стандартный `Error`.

Объект данной ошибки хранит ссылку на ошибку-причину, позволяя строить цепочку ошибок.

## Базовое использование
Ошибки инстанцируются одним из двух конструкторов:
```js
new BaseError(message: mixed, cause?: mixed)
new BaseError(cause?: Error)
```

Причины (`cause`), не являющиеся потомками `Error`, приводятся к ошибкам вызовом `new Error()`

Пример декларирования ошибки и её вариантов:
```js
import BaseError from '@yandex-market/error';

class MultipartError extends BaseError {}
class BusboyError extends MultipartError {}
class FilesLimitExceededError extends MultipartError {}
class FieldsLimitExceededError extends MultipartError {}
class FileSizeExceededError extends MultipartError {}
class ReadError extends MultipartError {}
```

Пример создания ошибки:
```js
new FileSizeExceededError(`Field: ${fieldName}`);
```

Пример оборачивания ошибки:
```js
try {
    ...
} catch (ex) {
    throw new BusboyError(ex);
}
```

Осторожно: `ex` имеет тип `any`, поэтому будет проходить любой вызов конструктора, даже некорректный.

## Расширенное использование
Для определения группы ошибок удобно использовать `BaseError.extend`:
```js
const SomeError = BaseError.extend({
    VariantA: ({a}: {a: string}) => `Some message: ${a}`,
    VariantB: () => 'Kek!',
});

new SomeError.VariantA({a: 'kek'});
```

Это эквивалентно следующему коду:
```js
class SomeError extends BaseError {}

class VariantAError extends SomeError {
    a: string;
    constructor({a}: {a: string}, cause?: mixed) {
        super(`Some message: ${a}`, cause);
        this.a = a;
    }
}

class VariantBError extends SomeError {
    message = 'Kek!';
}
```

Наследование отдельных вариантов ошибок (пока) не предусмотрено, однако сам `extend` можно вызывать от любой `BaseError` ошибки, но при этом должен сохраняться интерфейс конструкторов базового класса:
```js
class SomeError extends BaseError {}
const KekError = SomeError.extend({...});
const LolError = SomeError.extend({...});
```
