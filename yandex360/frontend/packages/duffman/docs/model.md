# Модель

**Модель** — это абстракция над запросом данных, она знает какие параметры нужно составить, чтобы получить данные, и как их потом обработать. Она не знает куда именно ей нужно сходить, об этом знает [сервис](./service.md).

Модель можно объявить как класс унаследованный от `duffman.Model` (предпочтительный новый способ), либо как простую функцию.

Не стоит вызывать модели напрямую. Лучше всего это делать через `core.request`, тогда запрос модели попадет в общий диспатчер и сможет вернуть закешированный результат, если модель уже запрашивалась в рамках сессии. Подробнее этот механизм описан в разделе [core](./core.md).

## Модель как класс

```ts
import { Model } from '@yandex-int/duffman';

class MyModelParams { ... }
class MyModelResult { ... }
type MyCore = ...;

class MyModel extends Model<MyModelParams, MyModelResult, MyCore> {
    async action(params: MyModelParams, core: MyCore): Promise<MyModelResult> {
        try {
            const data = await core.service('my-service')('/path');
            // Выносим обработку ответа в фильтр
            return filter(data);
        } catch (error) {
            // Обрабатываем ошибку на месте
            return error.reason;
        }
    }

    // Дополнительные флаги
    // Модели не нужна авторизация (автоматически отменяет проверку ckey)
    static noAuth = true;
    // Модель можно запрашивать без проверки ckey
    static noCkey = true;
    // Дополнительная предобработка параметров модели
    static modelParams = {
        userTicket: { hidden: true }
    };
}
```

## Модель как функция
Любая модель представляет из себя функцию, которая принимает два аргумента `params` и `core` и возвращает `Promise` с обработанным результатом ответа от сервера.

Сложную обработку ответа желательно выносить в фильтр.

```js
const filter = require('../filters/wmi/ninja_auth');

const model = async (params, core) => {
    try {
        const data = await core.service('wmi')('ninja_auth');
        // Выносим обработку ответа в фильтр
        return filter(data);
    } catch (error) {
        // Обрабатываем ошибку на месте
        return error.reason;
    }
};

module.exports = model;
```
У функциональной модели тоже можно задать флаги
```js
const {
    NO_AUTH,
    NO_CKEY,
    modelParams
} = require('@yandex-int/duffman').flags;

model[NO_AUTH] = true;
model[NO_CKEY] = true;
model[modelParams] = {
    userTicket: { hidden: true }
};
```
