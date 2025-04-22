# luster-messaging
One-to-many communication luster extension, with cookies and donuts.
Allows request-reply from one worker to rest (currently, including oneself).
Recipients replies aggregated and sended to requestor in timely manner.

# Setup
## install extension in application
`npm i -S git@github.yandex-team.ru:market/luster-messaging.git`

## enable extension
Luster [readme](https://github.com/nodules/luster/blob/master/README.md#annotated-example-of-configuration)

## Use API

# API
```javascript
require('luster-messaging').api
```

## request
Make request to all workers, and collect replies within collection timeout (plus transport).
```javascript
request(type, payload, timeout = 200)
```

### parameters
* type – request identifier, that will be listened by other workers
* payload – some data that will be transferred to recipients
* timeout – replies collection timeout

### returns
Promise that will be resolved with object of following format:

```javascript
[ 
    { workerId: 1, payload: 'test reply 1' }, 
    { workerId: 2, payload: 'test reply 2' } 
]
```
_If all workers replied within timeout_ 

```javascript
[
    { workerId: 1, payload: 'test reply 1' },
    { workerId: 2, error: 'timeout' }
]
```
_If some or all workers exceeded collection timeout, or other error occurred_

## onRequest
```javascript
onRequest(type, callback)
```

* type – request identifier, that will be requested by sender
* callback – function that will be called when event of specified type is received

```javascript
/**
 * @callback LusterMessagingClient~responseCallback
 * @param {object} payload
 * @returns {Promise}
 */
```
_callback definition_

Reject **must** be a string, or object with toJSON() method for correct serialization.

## Examples

### Listening for event 
```javascript
const lusterMessaging = require('luster-messaging');
lusterMessaging.api.onRequest('test', (payload) => {
    console.log('index test event', payload);
    return Promise.resolve('test reply');
});
```

### Making request
```javascript
const lusterMessaging = require('luster-messaging');
lusterMessaging.api.request('test', 'test payload')
    .then((data) => {
        console.log('api reply', data)
    }, (reason) => {
        console.log('api reject', reason);
    });

```


## Contribution
- git submodule update --init --recursive
- npm i
- make some ~~noise~~ code
- make some tests
- npm run codestyle
- npm run test
- PR
