## How to write api requests

You can use `server/lib/request` for making HTTP requests from Node JS,
it uses [got](https://www.npmjs.com/package/got) under the hood.

More specific request wrappers could be configured via `server/lib/request`. For example,
the following code will make requests to `http://foo-api.yandex.net`:

```typescript jsx
import {Response} from 'got';
import {Request} from 'express';
import request, {ApiRequestOptions} from 'server/lib/request';

type FooApiRequestOptions = Omit<ApiRequestOptions, 'prefixUrl'>;

function fooApiRequest(options: FooApiRequestOptions, req: Request): Promise<Response> {
    return request({
        ...options,
        headers: {
            ...options.headers,
            'X-Ya-User-Ticket': req.blackbox.userTicket,
            'X-Ya-Service-Ticket': req.tvm['foo-api']
        },
        prefixUrl: 'http://foo-api.yandex.net'
    });
}

export default fooApiRequest;
```

Now the following call

```typescript jsx
fooApiRequest({
    url: 'v1/entity/update',
    method: 'PATCH',
    searchParams: {property: 'bar'}
}, req);
```

will make `PATCH` request to `http://foo-api.yandex.net/v1/entity/update?property=bar`.
