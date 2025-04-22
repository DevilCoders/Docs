# express-async [![build status](https://badger.yandex-team.ru/github/maps/express-async/master/state.svg)](https://github.yandex-team.ru/maps/express-async/commits/master)

Async helpers for `express`.

## Installation

```sh
npm install --registry=https://npm.yandex-team.ru @yandex-int/express-async
```

## Usage

### Async middleware

Converts middleware, which returns promise, to regular `Express` middleware.

```ts
import * as express from 'express';
import {asyncMiddleware} from '@yandex-int/express-async';

const doSomething = asyncMiddleware(async (req, res) => {
    res.json(await getData());
});

express()
    .use(doSomething)
    .listen(3000);
```

Unlike regular `express` middleware, there is no `next` function. If the promise is rejected,
`next(err)` will be called with `err` being the value of the rejection. If the promise is fulfilled
and response header is not sent, `next` function will be called. Therefore, instead

```ts
function checkKey(req: Request, res: Response, next: NextFunction) {
    if (!await isKeyValid(req.query.key)) {
        next(Boom.unauthorized());
    } else {
        next();
    }
}
```

you can write

```ts
const checkKey = asyncMiddleware(async (req) => {
    if (!await isKeyValid(req.query.key)) {
        throw Boom.unauthorized();
    }
});
```
