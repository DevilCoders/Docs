# tvm [![build status](https://badger.yandex-team.ru/github/maps/tvm/master/state.svg)](https://github.yandex-team.ru/maps/tvm/commits/master)

High-level client for [TVM daemon](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon).

## Installation

```sh
npm install --registry=https://npm.yandex-team.ru @yandex-int/tvm
```

## Requirements

To work with this library you need install and run TVM daemon. See [documentation](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#kakzapustittvm-demona) for more information.

## Usage

This module provides class `Client`, which represents client of TVM daemon:

```ts
import * as tvm from '@yandex-int/tvm';

const client = new tvm.Client();
```

It's designed to work with minimal configuration. So, by default it expects that TVM daemon is ran
at address http://localhost:2 (environment variable `DEPLOY_TVM_TOOL_URL` is set by `Deploy` platform)
or http://localhost:1 (default for `Qloud` platform) and
environment variable `TVMTOOL_LOCAL_AUTHTOKEN` (default for `Deploy` platform)
or `QLOUD_TVM_TOKEN` (default for `Qloud` platform) is set.

For local development you can change this options:

```ts
const client = new tvm.Client({
    daemonBaseUrl: 'http://localhost:8001',
    token: 'some_token_value'
});
```

Using `client` instance you can perform different operations with tickets.

**Note:** you should have only once instance of `tvm.Client` for all requests.

### Service tickets

#### Check service ticket

```ts
async function checkTicket(ticket: string): Promise<void> {
    let ticketInfo: tvm.ServiceTicketInfo;
    try {
        ticketInfo = await client.checkServiceTicket(ticket);
    } catch (err) {
        if (err instanceof tvm.InvalidTicketError) {
            console.error(`Ticket is invalid`);
        } else {
            console.error(`Failed to check ticket: ${err}`);
        }
        return;
    }
    console.log(ticketInfo);
}
```

#### Get service tickets

If you need only one ticket you can use `Client#getServiceTicket` method:

```ts
const ticket = await client.getServiceTicket('dst');
console.log(ticket);
```

Parameter `dst` is alias of a destination service from TVM daemon configuration. For example, in the
following configuration:

```json
{
    "port": 8001,
    "clients": {
        "foo": {
            "secret": "",
            "self_tvm_id": 100500,
            "dsts": {
                "bar": {
                    "dst_id": 100501
                },
                "baz": {
                    "dst_id": 100502
                }
            }
        }
    }
}
```

valid destinations are `bar` and `baz`.

If you need to get tickets for several destinations, request them all at once:

```ts
const [ticketA, ticketB] = await Promise.all(client.getServiceTickets(['dstA', 'dstB']));
console.log(ticketA, ticketB);
```

Method `Client#getServiceTickets` returns array of promises, where each promise represents
service ticket. Note, that some of returned promises may be rejected. Therefore, if it's normal
situation for you, check state of each promise separately or use something like
[`Promise.allSettled`](https://github.com/tc39/proposal-promise-allSettled).

### User tickets

#### Check user ticket

```ts
async function checkTicket(ticket: string): Promise<void> {
    let ticketInfo: tvm.UserTicketInfo;
    try {
        ticketInfo = await client.checkUserTicket(ticket);
    } catch (err) {
        if (err instanceof tvm.InvalidTicketError) {
            console.error(`Ticket is invalid`);
        } else {
            console.error(`Failed to check ticket: ${err}`);
        }
        return;
    }
    console.log(ticketInfo);
}
```

### IDM Roles

[How to create IDM system](https://wiki.yandex-team.ru/users/pixel/kak-sozdat-svoju-sistemu-v-idm)

#### Check user roles

`alias` - service alias from `.tvm.json` or deploy config

```ts
async function checkUserRoles(alias: string, lookupRoles: string[]): Promise<void> {
    const ticket = req.headers['x-ya-user-ticket'] as string;
    const ticketInfo = await client.checkUserTicket(ticket);
    const roles = await client.getRoles(alias);

    const userRoles = roles.user?.[ticketInfo.defaultUid] || {};
    const hasAccess = lookupRoles.some((role) => userRoles[role]);
    if (!hasAccess) {
        throw new Error('Not enough access');
    }
}
```

#### Check service roles

`alias` - service alias from `.tvm.json` or deploy config

```ts
async function checkServiceRoles(alias: string, lookupRoles: string[]): Promise<void> {
    const ticket = req.headers['x-ya-service-ticket'] as string;
    const ticketInfo = await client.checkServiceTicket(ticket);
    const roles = await client.getRoles(alias);

    const serviceRoles = roles.service?.[ticketInfo.dst] || {};
    const hasAccess = lookupRoles.some((role) => serviceRoles[role]);
    if (!hasAccess) {
        throw new Error('Not enough access');
    }
}
```

### Caching

By default `Client` caches fetched tickets and results of checks on `10 minutes`. This is maximum
possible value.

### Logging

`Client` can log some useful debug information, e.g. requests and responses from TVM daemon. To
enable logging, provide `logger` option when instantiate `Client` class. Logger must implement
[Logger](src/lib/logger.ts) interface. For example, you can pass
[winston](https://github.com/winstonjs/winston) logger as is:

```ts
import * as tvm from '@yandex-int/tvm';
import {Logger} from 'winston';

const logger = new Logger();
const client = new tvm.Client({logger});
```
